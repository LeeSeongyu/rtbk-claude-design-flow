# WORKFLOW

이 문서는 `rtbk-claude-design-flow`를 **단계별 도구로 실행하는 방법**을 설명합니다.
자동 루프 없이, 각 단계를 사람이 필요할 때 호출합니다. 개요·역할은 `CLAUDE.md` 참고.

## 시작 전: 재료 준비 (사람)

`data/00-inputs/`에 재료를 넣습니다.

- `service-diagram/` — Service Diagram 이미지 + `service-diagram.md`
- `IA/` — 정보구조 이미지 + `IA.md`
- `wireframes/` — 기획초안 스케치/와이어프레임
- `competitors/` — 경쟁서비스 URL 목록/캡처 (`competitors.md`)
- `fruto-design/` — `fruto-source.md`에 비주얼 **값**의 원본 fruto Figma URL
- `carbon-format/` — 디자인 시스템 **형식**의 기준인 Carbon v11 양식 (파일 또는 URL)

## Step 1 — 서비스 분석 · `01-service-analyst`

- 입력: `service-diagram/`, `IA/` (이미지 + md)
- 산출물: `data/01-analysis/core-features.md`

## Step 2 — 기초 디자인 시스템 구축 · `02-design-system-builder`  ★ 화면보다 먼저

- 입력: **fruto Figma URL(값)** + **Carbon v11 양식(형식)**
- 하는 일:
  - Carbon v11 양식으로 문서 구조·토큰 네이밍·컴포넌트/상태 체계를 잡고
  - fruto Figma를 Figma MCP로 읽어 실제 값(색·타입·간격·컴포넌트 룩)을 채운다
  - fruto에 없는 값은 `미확인`으로 남긴다
- 산출물: `design-system` 스킬(RTBK Design System) + `data/02-design-system/`(추출 원자료·매핑표·변경 로그)
- 이 디자인 시스템은 이후 화면을 만들며 **계속 확장**된다 (living).

## Step 3 — 화면 정의 · `03-screen-designer`

- 입력: `core-features.md` + 경쟁서비스 URL/캡처 + **이미 구축된 디자인 시스템**
- 하는 일: Mobbin MCP + Playwright로 UX·패턴 조사, 영역별 → 화면별 정의.
  비주얼은 디자인 시스템 참조. 없는 컴포넌트는 `data/02-design-system/needed-additions.md`에 기록하고
  Step 2 재호출(추가) 요청.
- 산출물: `data/03-screens/screen-definitions.md`, `data/03-screens/wireframes.md`

## Step 4 — 마스터 디자인 브리프 · `04-brief-writer`

- 입력: Step 3 산출물 + 디자인 시스템
- 하는 일: 화면별 **최대 상세 description 프롬프트** 작성 (Figma·paper·Claude Design 공용)
- 산출물: `data/04-brief/{screen}.md`

## Step 5 — 3-way 시안 팬아웃

동일 브리프를 3개 도구에 각각 먹여 시안 생성.

- **5a Figma** · `05-figma-builder` — Figma MCP로 캔버스에 직접 빌드 → `data/05-candidates/figma/`
- **5b paper.design** — 브리프를 paper에 붙여넣어 생성 → `data/05-candidates/paper/`
- **5c Claude Design** — 브리프를 claude.ai/design에 붙여넣어 생성 → `data/05-candidates/claude-design/`

## ★ 게이트 — 사람 확인 + 커밋 (필수)

1. 3개 시안 비교 → 승자 선택·수정
2. **코드 소스는 항상 Figma** — 승자가 paper/Claude Design이면 Figma로 옮겨 확정
3. 확정된 Figma 상태를 `git commit`
4. **커밋 전까지 Step 6 진행 불가**

## Step 6 — 코드 생성 · `06-coder`

- 시작 전 확인: **확정·커밋된 Figma 화면**이 있는지 (없으면 중단)
- 입력: 확정된 Figma 화면 (Figma MCP 읽기) + 디자인 시스템
- 하는 일: Next.js + Tailwind 코드로 구현, 동작 검증
- 산출물: `data/06-code/`

## Step 7 — Codex 리뷰 (메인 세션)

- `/codex:review` → `data/07-review/review-N.md`
- `BLOCKER`/`MAJOR` → `/codex:rescue` 또는 `06-coder` 재호출(피드백 포함) → 최대 3회
- 3회 후에도 BLOCKER면 사람에게 보고. PASS 전까지 완료 아님. (자세히는 `CLAUDE.md`)

## 도구 준비 상태 확인

| 도구 | 확인 방법 | 없을 때 |
| --- | --- | --- |
| Figma MCP (읽기+쓰기) | 로그인·플러그인 연결 | 중단·안내 |
| Mobbin MCP | 연결 확인 (`https://api.mobbin.com/mcp`) | Step 3 레퍼런스 검색 생략·안내 |
| Playwright | 플러그인 확인 | Step 3 경쟁서비스 읽기 생략·안내 |
| Codex CLI | `codex@openai-codex` 활성 | Step 6·7 중단·설치 요청 |
