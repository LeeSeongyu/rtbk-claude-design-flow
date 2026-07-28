# rtbk-claude-design-flow

**사람이 넣은 재료로 프론트엔드 화면과 코드를 만들어내는 도구(toolkit)입니다.**
자동으로 도는 파이프라인이 아니라, 각 단계를 사람이 필요할 때 호출하는 단계별 도구 모음입니다.

한 문장 요약: **서비스 자료 → 핵심기능 → 화면정의·디자인시스템 → 상세 디자인 브리프 →
(Figma·paper·Claude Design) 3-way 시안 → 사람이 승자 선택 → Figma로 확정 → 코드 → Codex 리뷰.**

## 워크플로우 (6단계)

```
[사람 입력]  Service Diagram(img+md), IA(img+md), 기획 스케치, 경쟁서비스 URL, fruto Figma 파일
     │
Step 1  서비스 분석            01-service-analyst   → data/01-analysis/core-features.md
Step 2  화면정의 + 디자인시스템  02-screen-designer   → data/02-screens/*.md + design-system 스킬
        (Mobbin MCP + Playwright = UX·패턴 / fruto Figma = 비주얼 스타일)
Step 3  마스터 디자인 브리프    03-brief-writer      → data/03-brief/{screen}.md  (3개 도구 공용 프롬프트)
Step 4  3-way 시안 팬아웃
        ├─ 4a Figma       04-figma-builder (Figma MCP 직접 빌드) → data/04-candidates/figma/
        ├─ 4b paper.design (브리프 제공 → 생성)                  → data/04-candidates/paper/
        └─ 4c Claude Design(브리프 제공 → 생성)                  → data/04-candidates/claude-design/
     │
[★ 사람 게이트]  3개 시안 비교 → 승자 선택·수정 → 승자를 Figma로 확정 → git commit
     │
Step 5  코드 생성            05-coder             → data/05-code/  (Next.js + Tailwind)
Step 6  Codex 리뷰 (메인 세션) /codex:review       → data/06-review/review-N.md
```

## 에이전트

| 에이전트 | Step | 핵심 도구 | 산출물 |
| --- | --- | --- | --- |
| `01-service-analyst` | 1 서비스 분석 | 입력 자료 읽기 | `data/01-analysis/core-features.md` |
| `02-screen-designer` | 2 화면정의+디자인시스템 | Mobbin MCP, Playwright, **fruto Figma 읽기** | `data/02-screens/*.md` + `design-system` 스킬 채움 |
| `03-brief-writer` | 3 마스터 브리프 | (합성) | `data/03-brief/{screen}.md` |
| `04-figma-builder` | 4a Figma 시안 | **Figma MCP 쓰기** | Figma 캔버스 화면 + `data/04-candidates/figma/` |
| `05-coder` | 5 코드 생성 | Figma MCP 읽기 | `data/05-code/` |

> **Step 4b(paper) / 4c(Claude Design)**는 전용 에이전트가 없습니다. Step 3의 **공용 브리프**를
> 사람이 각 도구에 붙여넣어 생성하고, 결과를 `data/04-candidates/`에 저장합니다.
> (paper.design MCP가 확인되면 자동화로 승격 가능.)

> **Step 6(Codex 리뷰)**는 에이전트가 아니라 **메인 세션**이 담당합니다. 서브에이전트는
> `/codex:*` 슬래시 커맨드를 직접 호출할 수 없기 때문입니다 (아래 "코드 리뷰 오케스트레이션").

## 스킬

| 스킬 | 역할 |
| --- | --- |
| `design-system` | **fruto Design System** — 비주얼 토큰·컴포넌트 상태 규칙을 한 번 정의(HOW). Step 2가 채우고, Step 4·5가 참조. 비주얼 값의 출처는 사용자가 제공한 **fruto Figma 파일**. |

## 데이터 레이아웃

- `data/00-inputs/` — **사람이 넣는 재료** (아래 각 하위 폴더)
  - `service-diagram/` — Service Diagram 이미지 + `service-diagram.md`
  - `IA/` — 정보구조 이미지 + `IA.md`
  - `wireframes/` — 기획초안 스케치/와이어프레임
  - `competitors/` — 경쟁서비스 URL 목록/캡처
  - `fruto-design/` — 비주얼 스타일 원본인 **fruto Figma 파일 URL** (`fruto-source.md`)
- `data/01-analysis/` — Step 1: `core-features.md`
- `data/02-screens/` — Step 2: `screen-definitions.md`(구성요소·레이아웃), `wireframes.md`(화면별 설명)
- `data/03-brief/` — Step 3: 화면별 최대 상세 디자인 브리프(프롬프트)
- `data/04-candidates/{figma,paper,claude-design}/` — Step 4: 3-way 시안 결과·스크린샷·링크
- `data/05-code/` — Step 5: Next.js + Tailwind 코드
- `data/06-review/` — Step 6: `review-N.md`

## ★ 사람 게이트 (Step 4 → 5 사이, 필수)

1. 사람이 `data/04-candidates/`의 **Figma / paper / Claude Design 3개 시안을 비교**한다.
2. **승자 하나를 선택**하고, 필요하면 수정한다.
3. **코드의 소스는 항상 Figma다(옵션 A).** 승자가 paper나 Claude Design이면,
   그 시안을 참고해 **Figma에 옮겨 확정**한다 (Figma MCP 재빌드 또는 사람이 직접).
4. 확정된 Figma 상태를 **git commit** 한다.
5. **커밋 전까지 Step 5(코드 생성)로 넘어가지 않는다.** `05-coder`는 확정·커밋된 Figma가 없으면 중단한다.

## 코드 리뷰 오케스트레이션 (Step 6)

`05-coder`는 서브에이전트라 `/codex:*`를 직접 호출할 수 없으므로, 리뷰는 **메인 세션**이 오케스트레이션한다.

루프:
1. 메인 세션이 `/codex:review` 실행.
2. 결과를 `data/06-review/review-N.md`에 저장.
3. `BLOCKER`/`MAJOR`가 있으면 → `/codex:rescue` 또는 `05-coder`를 **리뷰 피드백 포함 재호출**해 수정 → 1번으로.
4. **최대 3회** 반복.
5. 3회 후에도 `BLOCKER`가 남으면 → **자동 종료하지 말고 사람에게 보고**한다. 임의로 완료 처리하지 않는다.

> **완료 규칙:** 리뷰가 **PASS**(BLOCKER/MAJOR 없음) 되기 전까지 완료로 표시하지 않는다.

## 필요 도구

- **Figma MCP** — 읽기(`get_design_context`, `get_variable_defs`) + 쓰기(프레임/노드 생성). Step 2(fruto 읽기), Step 4a(빌드), Step 5(읽기).
- **Mobbin MCP** — 디자인 레퍼런스 검색. Step 2.
- **Playwright** — 경쟁서비스 URL 접속해 화면/스타일/UX 로직 읽기. Step 2.
- **Codex CLI** (`codex@openai-codex`) — `/codex:review`, `/codex:rescue`. Step 6.

## 안전 규칙

- 각 에이전트는 **시작 전 필요한 도구/입력 존재 여부를 확인**하고, 없으면 **중단하고 사람에게 안내**한다.
- Figma **쓰기는 Step 4a(시안 빌드)와 게이트 확정에서만** 한다. Step 2·5의 Figma 접근은 읽기 전용.
- **디자인 시스템 비주얼은 fruto Figma 파일이 출처다.** 임의 색/폰트/간격 값을 지어내지 않는다.
- **사람 게이트를 건너뛰지 않는다.** 승자 확정·커밋 없이 코드로 진행하지 않는다.
