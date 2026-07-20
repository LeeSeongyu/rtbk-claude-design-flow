# rtbk-claude-design-flow

Figma 디자인을 입력으로 받아, 레퍼런스 케이스를 문서화하고, 화면을 코드로 구현한 뒤,
시각적 채점과 코드 리뷰를 거쳐 완료까지 이어지는 **디자인 → 코드 파이프라인**입니다.

## 파이프라인 개요

```
Figma URL
  └─▶ 00-figma-fetcher   구조 데이터 + 스크린샷 수집        → data/00-core-ui/
  └─▶ (사람) 레퍼런스 문서 작성                              → data/01-references/case-N/case-N.md
  └─▶ 01-case-deriver    케이스 도출 → 프롬프트 초안 → 1차 채점 → data/02-design-preceeding/
  └─▶ 02-coder           케이스별 화면 구현                  → data/03-code/
  └─▶ 코드 리뷰 오케스트레이션 (메인 세션)                  → data/04-review/
```

## 에이전트

| 에이전트 | 역할 | 산출물 |
| --- | --- | --- |
| `00-figma-fetcher` | Figma MCP로 구조 데이터를 가져오고 Playwright로 스크린샷 캡처 (읽기 전용) | `data/00-core-ui/` |
| `01-case-deriver` | 레퍼런스 문서 확인(사람 작성, Step 0) → 케이스 도출(Step 1) → 프롬프트 초안 생성(Step 2) → 결과 1차 채점(Step 3) | `data/02-design-preceeding/` |
| `02-coder` | 케이스별 화면을 실제 코드로 구현 | `data/03-code/` |

## 스킬

| 스킬 | 역할 |
| --- | --- |
| `design-system` | 코어 UI 토큰 + 컴포넌트 상태별 스타일·인터랙션을 한 번 정의(HOW). `02-coder`·`01-case-deriver`가 공통 참조 |
| `visual-verdict` | 생성 화면을 레퍼런스와 비교해 score/verdict를 JSON으로 반환 (통과 기준 85점) |

## 데이터 레이아웃

- `data/00-core-ui/` — Figma에서 수집한 코어 UI 구조 데이터와 스크린샷
- `data/01-references/case-N/` — 레퍼런스 이미지와 **사람이 작성한** `case-N.md`(출처·시나리오·기능·신뢰도)
- `data/02-design-preceeding/` — `case-screens.md`(케이스별 상태 대장) + `case-N/`(도출된 화면 정의 + `prompt.md` 프롬프트 초안)
- `data/03-code/` — 구현된 코드
- `data/04-review/` — `review-{N}.md` 코드 리뷰 결과

## 코드 리뷰 오케스트레이션

`02-coder`는 **서브에이전트라서 `/codex:*` 슬래시 커맨드를 직접 호출할 수 없습니다.**
따라서 코드 리뷰는 반드시 **메인 세션**이 오케스트레이션합니다.

루프 (케이스 N에 대해):

1. **리뷰 실행** — 메인 세션이 `/codex:review`를 실행한다.
2. **결과 저장** — 리뷰 결과를 `data/04-review/review-{N}.md`에 저장한다.
3. **판정 분기**
   - `BLOCKER` 또는 `MAJOR`가 있으면 → `/codex:rescue`를 실행하거나,
     `02-coder`를 **리뷰 피드백을 포함하여 재호출**해 수정한다.
   - 수정 후 다시 1번으로 돌아간다.
4. **반복 제한** — 위 루프는 **최대 3회** 반복한다.
5. **3회 후에도 BLOCKER가 남으면** → **자동으로 종료하지 말고 사람에게 보고**한다.
   판단을 사람에게 넘기고, 임의로 완료 처리하지 않는다.

> **완료 규칙:** 리뷰가 **PASS** 될 때까지 해당 케이스를 완료로 표시하지 않는다.
> `case-screens.md`의 상태는 PASS 시점에만 "완료"로 갱신한다.

## 상태 값 규약 (`data/02-design-preceeding/case-screens.md`)

- `생성중` — 화면 구현 진행 중 또는 1차 채점 미통과(85점 미만)
- `검토중` — 1차 채점 통과(85점 이상), 코드 리뷰 대기/진행 중
- `완료` — 코드 리뷰 PASS

## 안전 규칙

- Figma에 대한 **쓰기 작업은 절대 하지 않는다** (읽기·스크린샷 전용).
- 로그인 세션이 없으면 진행을 **중단하고 사람에게 안내**한다.
- 필수 도구(Figma MCP, Playwright, Codex CLI 플러그인)가 없으면 중단하고 설치를 요청한다.
- **`case-N.md`(레퍼런스 문서)는 사람이 작성한다.** 에이전트가 임의로 작성·덮어쓰지 않으며,
  이미지가 있는데 문서가 없으면 진행을 중단하고 사람에게 작성을 요청한다.
