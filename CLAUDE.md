# rtbk-claude-design-flow

**사람이 넣은 재료로 프론트엔드 화면과 코드를 만들어내는 도구(toolkit)입니다.**
자동으로 도는 파이프라인이 아니라, 각 단계를 사람이 필요할 때 호출하는 단계별 도구 모음입니다.

한 문장 요약: **서비스 자료 → 핵심기능 → (먼저) 기초 디자인 시스템 → 화면 정의 → 상세 브리프 →
(Figma·paper·Claude Design) 3-way 시안 → 사람이 승자 선택 → Figma로 확정 → 코드 → Codex 리뷰.**

RTBK 화면은 아직 없고 기획만 있습니다. 그래서 **화면을 만들기 전에 기초 디자인 시스템을 먼저 구축**하고,
화면을 만들며 필요한 요소를 추가하며 **디자인 시스템이 계속 확장(living)**됩니다.

## 워크플로우 (7단계)

```
[사람 입력]  Service Diagram(img+md), IA(img+md), 기획 스케치, 경쟁서비스 URL,
             fruto Figma(비주얼 값), Carbon v11 양식(형식)
     │
Step 1  서비스 분석            01-service-analyst        → data/01-analysis/core-features.md
Step 2  기초 디자인 시스템 구축  02-design-system-builder  → design-system 스킬 + data/02-design-system/
        (값 = fruto Figma / 형식 = Carbon v11 양식) ★ 화면보다 먼저
Step 3  화면 정의             03-screen-designer        → data/03-screens/*.md
        (Mobbin MCP + Playwright = UX·패턴 / 비주얼 = 디자인 시스템 참조)
Step 4  마스터 디자인 브리프    04-brief-writer           → data/04-brief/{screen}.md  (3개 도구 공용)
Step 5  3-way 시안 팬아웃
        ├─ 5a Figma       05-figma-builder (Figma MCP 직접 빌드) → data/05-candidates/figma/
        ├─ 5b paper.design (브리프 제공 → 생성)                  → data/05-candidates/paper/
        └─ 5c Claude Design(브리프 제공 → 생성)                  → data/05-candidates/claude-design/
     │
[★ 사람 게이트]  3개 시안 비교 → 승자 선택·수정 → 승자를 Figma로 확정 → git commit
     │
Step 6  코드 생성            06-coder                  → data/06-code/  (Next.js + Tailwind)
Step 7  Codex 리뷰 (메인 세션) /codex:review            → data/07-review/review-N.md
```

> 화면을 만들며 새 컴포넌트·토큰이 필요하면 **디자인 시스템에 되먹임(추가)** 한다 (Step 3·5·6 → Step 2 재호출).

## 에이전트

| 에이전트 | Step | 핵심 도구 | 산출물 |
| --- | --- | --- | --- |
| `01-service-analyst` | 1 서비스 분석 | 입력 자료 읽기 | `data/01-analysis/core-features.md` |
| `02-design-system-builder` | 2 기초 디자인 시스템 | **fruto Figma 읽기** + Carbon v11 양식 | `design-system` 스킬 + `data/02-design-system/` |
| `03-screen-designer` | 3 화면 정의 | Mobbin MCP, Playwright | `data/03-screens/*.md` |
| `04-brief-writer` | 4 마스터 브리프 | (합성) | `data/04-brief/{screen}.md` |
| `05-figma-builder` | 5a Figma 시안 | **Figma MCP 쓰기** | Figma 캔버스 화면 + `data/05-candidates/figma/` |
| `06-coder` | 6 코드 생성 | Figma MCP 읽기 | `data/06-code/` |

> **Step 5b(paper) / 5c(Claude Design)**는 전용 에이전트가 없습니다. Step 4의 **공용 브리프**를
> 사람이 각 도구에 붙여넣어 생성하고, 결과를 `data/05-candidates/`에 저장합니다.
> (paper.design MCP가 확인되면 자동화로 승격 가능.)

> **Step 7(Codex 리뷰)**는 에이전트가 아니라 **메인 세션**이 담당합니다. 서브에이전트는
> `/codex:*` 슬래시 커맨드를 직접 호출할 수 없기 때문입니다 (아래 "코드 리뷰 오케스트레이션").

## 스킬

| 스킬 | 역할 |
| --- | --- |
| `design-system` | **RTBK Design System** (살아있는 문서). 비주얼 토큰·컴포넌트 상태 규칙을 정의(HOW). **값의 출처는 fruto Figma, 형식의 출처는 Carbon v11 양식.** Step 2가 owner로 채우고, Step 3~6이 참조하며 필요 요소를 되먹인다. |

## 데이터 레이아웃

- `data/00-inputs/` — **사람이 넣는 재료**
  - `service-diagram/` — Service Diagram 이미지 + `service-diagram.md`
  - `IA/` — 정보구조 이미지 + `IA.md`
  - `wireframes/` — 기획초안 스케치/와이어프레임
  - `competitors/` — 경쟁서비스 URL 목록/캡처
  - `fruto-design/` — 비주얼 **값**의 출처인 fruto Figma URL (`fruto-source.md`)
  - `carbon-format/` — 디자인 시스템 **형식**의 출처인 Carbon v11 양식 (`README.md` 참고)
- `data/01-analysis/` — Step 1: `core-features.md`
- `data/02-design-system/` — Step 2: fruto 추출 원자료, Carbon↔fruto 매핑표, `needed-additions.md`, 변경 로그
  (디자인 시스템 정본은 `design-system` 스킬에 있음)
- `data/03-screens/` — Step 3: `screen-definitions.md`, `wireframes.md`
- `data/04-brief/` — Step 4: 화면별 최대 상세 디자인 브리프
- `data/05-candidates/{figma,paper,claude-design}/` — Step 5: 3-way 시안 결과·스크린샷·링크
- `data/06-code/` — Step 6: Next.js + Tailwind 코드
- `data/07-review/` — Step 7: `review-N.md`

## 디자인 시스템 (값 = fruto / 형식 = Carbon v11 / 살아있음)

- **값** — 색·타이포·간격·컴포넌트 룩의 실제 값은 **fruto Figma**에서 추출한다.
- **형식** — 토큰 네이밍·컴포넌트 분류·상태 체계 등 문서의 짜임새는 **Carbon Design System v11 양식**을 따른다.
- **살아있음** — 화면을 만들며 새 요소가 필요하면 `02-design-system-builder`가 Carbon v11 형식에 맞춰
  편입하고 fruto 스타일로 값을 정한다. 값이 fruto에 없으면 `미확인`으로 두고 사람이 확정한다.
- 다른 에이전트는 스타일을 임의로 지어내지 않고 `data/02-design-system/needed-additions.md`에 요청을 남긴다.

## ★ 사람 게이트 (Step 5 → 6 사이, 필수)

1. 사람이 `data/05-candidates/`의 **Figma / paper / Claude Design 3개 시안을 비교**한다.
2. **승자 하나를 선택**하고, 필요하면 수정한다.
3. **코드의 소스는 항상 Figma다(옵션 A).** 승자가 paper나 Claude Design이면,
   그 시안을 참고해 **Figma에 옮겨 확정**한다 (Figma MCP 재빌드 또는 사람이 직접).
4. 확정된 Figma 상태를 **git commit** 한다.
5. **커밋 전까지 Step 6(코드 생성)로 넘어가지 않는다.** `06-coder`는 확정·커밋된 Figma가 없으면 중단한다.

## 코드 리뷰 오케스트레이션 (Step 7)

`06-coder`는 서브에이전트라 `/codex:*`를 직접 호출할 수 없으므로, 리뷰는 **메인 세션**이 오케스트레이션한다.

루프:
1. 메인 세션이 `/codex:review` 실행.
2. 결과를 `data/07-review/review-N.md`에 저장.
3. `BLOCKER`/`MAJOR`가 있으면 → `/codex:rescue` 또는 `06-coder`를 **리뷰 피드백 포함 재호출**해 수정 → 1번으로.
4. **최대 3회** 반복.
5. 3회 후에도 `BLOCKER`가 남으면 → **자동 종료하지 말고 사람에게 보고**한다. 임의로 완료 처리하지 않는다.

> **완료 규칙:** 리뷰가 **PASS**(BLOCKER/MAJOR 없음) 되기 전까지 완료로 표시하지 않는다.

## 필요 도구

- **Figma MCP** — 읽기(`get_design_context`, `get_variable_defs`) + 쓰기(프레임/노드 생성).
  Step 2(fruto 읽기), Step 5a(빌드), Step 6(읽기).
- **Mobbin MCP** — 디자인 레퍼런스 검색. Step 3.
- **Playwright** — 경쟁서비스 URL 접속해 화면/스타일/UX 로직 읽기. Step 3.
- **Codex CLI** (`codex@openai-codex`) — `/codex:review`, `/codex:rescue`. Step 7.

## 안전 규칙

- 각 에이전트는 **시작 전 필요한 도구/입력 존재 여부를 확인**하고, 없으면 **중단하고 사람에게 안내**한다.
- Figma **쓰기는 Step 5a(시안 빌드)와 게이트 확정에서만** 한다. Step 2·6의 Figma 접근은 읽기 전용.
- **디자인 시스템 값의 출처는 fruto, 형식의 출처는 Carbon v11.** 둘 다 임의로 대체하지 않고,
  값이 없으면 `미확인`으로 남긴다.
- **사람 게이트를 건너뛰지 않는다.** 승자 확정·커밋 없이 코드로 진행하지 않는다.
