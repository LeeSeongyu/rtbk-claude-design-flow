# HARNESS

이 문서는 `rtbk-claude-design-flow` 파이프라인을 **실행하는 방법(하네스)**을 정의합니다.
각 단계는 앞 단계의 산출물이 존재해야 진행됩니다.

## 사전 요구사항

- **Figma MCP** — `get_metadata`, `get_design_context`, `get_variable_defs` 사용 가능
- **Playwright 플러그인** — Figma URL 스크린샷 캡처
- **Codex CLI 플러그인** (`codex@openai-codex`) — 코드 리뷰(`/codex:review`, `/codex:rescue`)
- **Figma 로그인 세션** — 없으면 중단

## 실행 순서

### 1. Figma 수집 — `00-figma-fetcher`
- Figma MCP로 구조 데이터(metadata / design context / variable defs)를 가져온다.
- Playwright로 Figma URL에 접속해 스크린샷을 캡처한다.
- 산출물: `data/00-core-ui/`
- **쓰기 금지 / 세션 없으면 중단.**

### 2. 케이스 도출 — `01-case-deriver`
- **Step 0** 레퍼런스 케이스 문서화 → `data/01-references/case-N/case-N.md`
- **Step 1** 케이스 도출 → `data/02-design-preceeding/case-N/`, `case-screens.md`
- **Step 2** 결과 1차 채점 (`visual-verdict`) → 상태 갱신 + `verdict.md`

### 3. 코드 구현 — `02-coder`
- 케이스별 화면을 코드로 구현한다.
- `design-system` 스킬로 코어 UI 토큰·컴포넌트를 일관되게 적용한다.
- 산출물: `data/03-code/`
- **시작 전 Codex CLI 플러그인 활성화 여부 확인.**

### 4. 코드 리뷰 오케스트레이션 — 메인 세션
- `/codex:review` → `data/04-review/review-{N}.md`
- `BLOCKER`/`MAJOR` → `/codex:rescue` 또는 `02-coder` 재호출(피드백 포함)
- 최대 3회. 이후에도 BLOCKER면 사람에게 보고.
- **PASS 전까지 완료로 표시하지 않는다.** (자세한 규칙은 `CLAUDE.md` 참고)

## 게이트 (품질 관문)

| 게이트 | 기준 | 미통과 시 |
| --- | --- | --- |
| 1차 채점 | `visual-verdict` score ≥ 85 | 상태 `생성중` 유지, 재구현 |
| 코드 리뷰 | `/codex:review` PASS (BLOCKER/MAJOR 없음) | 최대 3회 수정, 이후 사람 보고 |

## pre-commit

`.husky/pre-commit`가 커밋 전 기본 점검을 수행합니다.
