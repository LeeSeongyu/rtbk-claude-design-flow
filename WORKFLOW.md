# WORKFLOW

이 문서는 `rtbk-claude-design-flow`를 **단계별 도구로 실행하는 방법**을 설명합니다.
자동 루프 없이, 각 단계를 사람이 필요할 때 호출합니다. 개요·역할은 `CLAUDE.md` 참고.

## 시작 전: 재료 준비 (사람)

`data/00-inputs/`에 재료를 넣습니다.

- `service-diagram/` — Service Diagram 이미지 + `service-diagram.md`
- `IA/` — 정보구조 이미지 + `IA.md`
- `wireframes/` — 기획초안 스케치/와이어프레임
- `competitors/` — 경쟁서비스 URL 목록/캡처 (`competitors.md`에 URL 정리)
- `fruto-design/` — `fruto-source.md`에 비주얼 스타일 원본 **fruto Figma 파일 URL** 기입

## Step 1 — 서비스 분석 · `01-service-analyst`

- 입력: `service-diagram/`, `IA/` (이미지 + md)
- 하는 일: 자료를 종합해 서비스 핵심 기능을 정의
- 산출물: `data/01-analysis/core-features.md`

## Step 2 — 화면 정의 + 디자인 시스템 · `02-screen-designer`

- 입력: `core-features.md` + 경쟁서비스 URL/캡처 + **fruto Figma 파일 URL**
- 하는 일:
  - **UX·패턴** — Mobbin MCP로 실제 앱 레퍼런스 검색 + Playwright로 경쟁서비스 화면 읽기
  - **비주얼 스타일** — fruto Figma 파일을 Figma MCP로 읽어 토큰·컴포넌트 스타일 추출
  - 영역별 → 화면별로 3가지 도출
- 산출물:
  - `data/02-screens/screen-definitions.md` — 화면별 구성요소·내역·레이아웃
  - `design-system` 스킬(fruto Design System) — 컴포넌트 상태별 스타일·토큰 (비주얼 출처: fruto)
  - `data/02-screens/wireframes.md` — 화면별 와이어프레임 설명

## Step 3 — 마스터 디자인 브리프 · `03-brief-writer`

- 입력: Step 2 산출물 전부
- 하는 일: 화면별로 **최대 상세한 description 프롬프트**를 작성 (Figma·paper·Claude Design 공용)
- 산출물: `data/03-brief/{screen}.md`

## Step 4 — 3-way 시안 팬아웃

동일한 브리프를 3개 도구에 각각 먹여 시안을 생성합니다.

- **4a Figma** · `04-figma-builder` — Figma MCP로 캔버스에 직접 빌드 → `data/04-candidates/figma/`
- **4b paper.design** — 브리프를 paper에 붙여넣어 생성 → `data/04-candidates/paper/`
- **4c Claude Design** — 브리프를 claude.ai/design에 붙여넣어 생성 → `data/04-candidates/claude-design/`

> 각 후보 폴더에 결과 스크린샷·링크·메모를 저장한다.

## ★ 게이트 — 사람 확인 + 커밋 (필수)

1. 3개 시안 비교 → 승자 선택·수정
2. **코드 소스는 항상 Figma** — 승자가 paper/Claude Design이면 Figma로 옮겨 확정
3. 확정된 Figma 상태를 `git commit`
4. **커밋 전까지 Step 5 진행 불가**

## Step 5 — 코드 생성 · `05-coder`

- 시작 전 확인: **확정·커밋된 Figma 화면**이 있는지 (없으면 중단)
- 입력: 확정된 Figma 화면 (Figma MCP 읽기) + `design-system` 스킬
- 하는 일: Next.js + Tailwind 코드로 구현, 동작 검증
- 산출물: `data/05-code/`

## Step 6 — Codex 리뷰 (메인 세션)

- `/codex:review` → `data/06-review/review-N.md`
- `BLOCKER`/`MAJOR` → `/codex:rescue` 또는 `05-coder` 재호출(피드백 포함) → 최대 3회
- 3회 후에도 BLOCKER면 사람에게 보고. PASS 전까지 완료 아님. (자세히는 `CLAUDE.md`)

## 도구 준비 상태 확인

| 도구 | 확인 방법 | 없을 때 |
| --- | --- | --- |
| Figma MCP (읽기+쓰기) | 로그인·플러그인 연결 | 중단·안내 |
| Mobbin MCP | 연결 확인 (`https://api.mobbin.com/mcp`) | Step 2 레퍼런스 검색 생략·안내 |
| Playwright | 플러그인 확인 | Step 2 경쟁서비스 읽기 생략·안내 |
| Codex CLI | `codex@openai-codex` 활성 | Step 6 중단·설치 요청 |
