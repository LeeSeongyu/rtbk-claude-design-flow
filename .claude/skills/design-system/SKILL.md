---
name: design-system
description: RTBK Design System — Carbon Design System v11의 요소별 카탈로그(토큰·컴포넌트 구조)를 골격으로 삼고, fruto와 유사한 요소는 fruto 비주얼로 대체, 없는 것은 Carbon 기본값 유지. 화면을 만들며 확장되는 살아있는 문서. 02-design-system-builder가 owner, 03~06이 참조.
---

# RTBK Design System

**골격 = Carbon Design System v11**(토큰 카테고리 + 컴포넌트 카탈로그). 각 요소에 대해:

- **fruto에 유사 요소가 있으면 → fruto 비주얼로 대체(substitute).** 태그 `[fruto]`
- **fruto에 없고 Carbon에만 있으면 → Carbon v11 기본값 유지.** 태그 `[carbon]`
- **fruto가 Carbon과 형태가 다르면(적응 필요) → fruto 우선하되 차이 명시.** 태그 `[fruto-adapt]`
- **아직 값 미확정(관찰 추정/미관찰) →** 태그 `[미확인]`

> 값 출처: 비주얼 값은 `data/02-design-system/fruto-visual-extraction.md`(관찰 추정). 구조·네이밍·기본값은 Carbon v11.
> 정확한 hex/폰트/치수는 후속 확정 대상(사람 또는 특정 노드 정밀 추출).

```
component-rules-verified: false   # fruto 값이 관찰 추정치라 미확정. 정밀값 확정 시 true.
```

## 살아있는 문서 (Living)

- 화면(Step 3~6)을 만들며 필요한 컴포넌트가 나오면 **Carbon 카탈로그에서 해당 요소를 찾아** 추가하고,
  fruto 유사물이 있으면 대체, 없으면 Carbon 기본값을 쓴다. 새 요소 요청은 `data/02-design-system/needed-additions.md`.
- 모든 추가·변경은 하단 **변경 로그**에 기록.

---

# 1. Foundations (Carbon 구조 · fruto 값)

## 1.1 Color tokens (Carbon 역할 기반 네이밍 · fruto 값 대체) `[fruto]`

> Carbon의 역할 토큰 네이밍을 쓰고, 값은 fruto 관찰값으로 매핑. 값은 모두 `[미확인]`(관찰 추정) — 정밀 확정 필요.

| Carbon 토큰 | fruto 값(추정) | 비고 |
|---|---|---|
| `$background` | `#EEF0FA`(인증) / `#FFFFFF`(앱) | 라이트 라벤더 배경 |
| `$layer-01` | `#FFFFFF` | 카드·콘텐츠 표면 |
| `$layer-02` | `#F1F2F8` | 인풋 fill·보조 표면 |
| `$field-01` | `#F1F2F8` / `#FFFFFF` | 인풋 배경 |
| `$border-subtle` | `#E9EAF0` | 구분선·인풋 보더 |
| `$text-primary` | `#22242F` | 딥네이비 |
| `$text-secondary` | `#6B7280` | 보조 텍스트 |
| `$text-placeholder` | `#A0A3B1` | 플레이스홀더/disabled |
| `$text-on-color` | `#FFFFFF` | 컬러 배경 위 텍스트 |
| `$link-primary` | `#5A5CE0` | 인디고 링크 |
| `$interactive` / `$button-primary` | `#5A5CE0` | **브랜드 Primary(인디고)** |
| `$button-primary-hover` | `#4A4CD0`(추정) | hover |
| `$support-success` | `#22C55E` | 정상 |
| `$support-warning` | `#EAB308` | 경고 |
| `$support-error` | `#EF4444` | 위험 |
| `$layer-accent`(테이블 헤더) | `#EEEFF9` | 라이트 라벤더 헤더 |

- **테마**: Carbon은 White/Gray10/Gray90/Gray100. RTBK는 **White(라이트) 단일**로 시작 `[fruto]`. 다크는 후속 `[carbon]`.
- **차트 categorical** `[fruto]`: 인디고 `#5A5CE0` / 앰버 / 코랄 / 그린 / 퍼플 / 틸 (6색, `@carbon/charts` 팔레트를 fruto 색으로 대체).

## 1.2 Typography (Carbon type set · fruto 값) `[fruto-adapt]`

- **폰트**: Pretendard 계열(추정) `[미확인]`. Carbon 기본은 IBM Plex Sans → **fruto 폰트로 대체**.
- Carbon type set 네이밍 유지, 값은 fruto 스케일로:

| Carbon set | 용도 | fruto 값(추정) |
|---|---|---|
| `display-01` | 페이지 타이틀 | ~24–28 / Bold |
| `heading-03` | 섹션·카드 타이틀 | ~18–20 / SemiBold |
| `heading-01` | 서브 타이틀 | ~16 / Medium |
| `body-01` | 본문 | ~14–15 / Regular, lh ≥ 1.5 |
| `label-01` | 라벨·네비 | ~13–15 / Medium |
| `caption-01` | 캡션·메타 | ~12–13 / Regular |

## 1.3 Spacing (Carbon spacing scale 유지) `[carbon]`

- Carbon `spacing-01`(0.125rem) … `spacing-13`(10rem), 8px mini-unit 기반. fruto도 8px 리듬이라 **Carbon 스케일 그대로 사용**.

## 1.4 Radius `[fruto-adapt]`

- Carbon은 각진(작은 radius) 편 → **fruto는 더 둥금**으로 대체:
  - 컨트롤(버튼·인풋): 인증은 pill, 앱 내 ~12–16px. `radius-control ≈ 12` (인증 variant는 pill) `[미확인]`
  - 카드·테이블: ~8–12px `radius-container ≈ 10`
  - 칩/배지: pill

## 1.5 Motion `[carbon]`

- Carbon motion 토큰 유지: `fast-01/02`, `moderate-01/02`, easing `productive`/`expressive`. (fruto 미관찰 → Carbon 기본)

## 1.6 Grid / Elevation `[carbon]`

- Carbon 2x Grid, elevation(그림자) 토큰 유지. fruto 카드 그림자 미세 → Carbon `[미확인]`.

---

# 2. Components (Carbon 카탈로그 순 · fruto 대체 표기)

> 각 컴포넌트: **상태별 스타일은 위 토큰 참조.** hover/focus/pressed 등 fruto 미관찰 상태는 Carbon 기본 규칙 사용.

## 2.1 Button `[fruto]`
- Variant(Carbon): primary / secondary / tertiary / ghost / danger.
- fruto 대체: **primary = 인디고(`$button-primary`) + 흰 텍스트 + 둥근(인증 pill)**. disabled = `$layer-02` bg + `$text-placeholder`(관찰됨).
- hover/focus/active: Carbon 규칙(hover=진한 인디고, focus=focus ring) `[carbon 기본]`.
- secondary/tertiary/ghost/danger: Carbon 기본 구조 + fruto 색 대입.

## 2.2 Text Input / Textarea `[fruto]`
- fruto: 둥근 필드, 기본 `$field-01`, 플레이스홀더 `$text-placeholder`. 두 톤 관찰(흰색/회색fill) → 기본=회색fill.
- Password: reveal(눈) 아이콘 관찰.
- focus/error/disabled 상태: Carbon 규칙 + fruto 색(error=`$support-error`) `[carbon 기본]`.

## 2.3 Checkbox `[fruto-adapt]`
- fruto는 **원형 체크**(Carbon은 사각) — fruto 형태 우선, 차이 명시. checked=인디고.

## 2.4 Radio Button `[carbon]`
- fruto 미관찰 → Carbon 기본(색만 인디고).

## 2.5 Toggle / Slider / Number input / File uploader `[carbon]`
- fruto 미관찰 → Carbon v11 기본 유지(브랜드 색만 인디고 대입).

## 2.6 Dropdown / Select `[fruto]`
- fruto: **pill형 필터 드롭다운**(라벨 + ▾, 라이트 보더). Carbon Dropdown 구조 + fruto pill 스타일.

## 2.7 Search `[fruto]`
- fruto: 둥근 인풋 + 검색 아이콘("이름 검색"). Carbon Search 구조 + fruto 스타일.

## 2.8 Tabs `[fruto]`
- fruto: **밑줄형 탭**, active=인디고 텍스트+인디고 밑줄. 2차 탭(서브탭)도 동일 패턴. Carbon "line" Tabs로 매핑.

## 2.9 Tag / Badge `[fruto]`
- fruto: **인디고 pill 배지**(예 D-19). Carbon Tag → 인디고 대체. 상태 Tag는 아래 Status.

## 2.10 Status indicator `[fruto]`
- fruto: **색점 + 텍스트** — 정상(녹색)/경고(앰버)/위험(빨강). Carbon엔 정확 대응 없음 → fruto 패턴 채택(Carbon Tag/“status” 응용).

## 2.11 Data Table `[fruto]`
- fruto: 정렬 가능 헤더(▾), 행 하단 구분선, 라이트 라벤더 헤더(`$layer-accent`), 합계행 강조, 셀 내 status/badge.
- Carbon Data Table 구조 + fruto 스타일. 정렬/선택/확장 등 세부는 Carbon 기본.

## 2.12 Pagination `[carbon]`
- fruto 미관찰(리스트 "총 510명"만) → Carbon Pagination 기본 + 인디고.

## 2.13 Date Picker `[fruto]`
- fruto: **캘린더 팝오버**(월 네비, 오늘=인디고, 시작/종료일 인풋) + **퀵레인지 칩**(오늘/어제/이번주/지난주/이번달), 취소/확인 버튼. Carbon Date Picker(range) + fruto 스타일.

## 2.14 Overflow Menu `[fruto]`
- fruto: `…` 오버플로우. Carbon Overflow Menu.

## 2.15 Modal / Dialog `[fruto-adapt]`
- fruto 팝오버(피커/메뉴) 관찰, 풀 Modal 미관찰 → Carbon Modal 구조 + fruto 색·radius. RTBK 팝업(검토/Note 등) 다수 → 중요.

## 2.16 Notification / Toast `[carbon]`
- fruto 미관찰 → Carbon Inline/Toast Notification 기본 + support 색(success/warning/error) fruto 값.

## 2.17 Progress Indicator (Stepper) `[fruto]`
- fruto: **번호 스텝퍼**(1–5). 완료=인디고 외곽+인디고 번호, 현재=인디고 채움+흰 번호+굵은 라벨, 이후=회색. Carbon Progress Indicator로 매핑.

## 2.18 Content Switcher / Segmented `[fruto]`
- fruto: 남/여 같은 세그먼트 선택. Carbon Content Switcher.

## 2.19 Breadcrumb / Link (back) `[fruto]`
- fruto: `‹ 목록으로` 뒤로가기 링크. Carbon Breadcrumb/Link + chevron.

## 2.20 UI Shell (Header / Nav) `[fruto]`
- fruto: 상단 헤더 — 로고 + 가로 네비(active=인디고 텍스트+밑줄) + 우측 사용자 인사·아바타. Carbon UI Shell Header로 매핑.
  - RTBK 적용: GNB에 `부가가치세` / `홈택스 연동`(업체) 같은 위계, 회계 측 하위 탭.

## 2.21 Charts `[fruto]`
- fruto: 막대차트 + 범례(색점). Carbon `@carbon/charts` + fruto categorical 팔레트.

## 2.22 그 외 Carbon 컴포넌트 `[carbon]`
- Accordion / Tile / Tooltip / Loading / Structured list / Code snippet 등 fruto 미관찰 → **Carbon v11 기본 유지**, 브랜드 색(인디고)·radius·폰트만 fruto 토큰 대입.

---

## 사용 규칙

- **`05-figma-builder`** — Figma 빌드 시 여기 토큰/컴포넌트 사용. `[carbon]` 요소는 Carbon 기본 형태, `[fruto]`는 fruto 스타일.
- **`06-coder`** — 구현 스택: Next.js + Tailwind. Carbon 토큰 네이밍을 Tailwind 토큰으로 매핑, 값은 위 표(fruto). `@carbon/react`를 쓸 경우 테마 토큰을 fruto 값으로 오버라이드. 임의 hex 금지.
- **`04-brief-writer`** — 브리프에 이 토큰/컴포넌트를 인용.
- **새 컴포넌트** — Carbon 카탈로그에서 찾아 여기 추가 후 사용.

## 확정 필요 (우선순위)

1. **정확한 색 hex** (관찰 추정 → 정밀값). 특히 Primary 인디고, support 3색, 배경/보더.
2. **폰트 패밀리**(Pretendard? 확인).
3. **Radius·컨트롤 높이·간격 수치**.
4. **인터랙션 상태 색**(hover/focus/pressed) — 미관찰분.

## 변경 로그 (Living)

| 날짜 | 변경 | 출처/사유 | 담당 |
|---|---|---|---|
| 2026-07-28 | 초기 구축: Carbon v11 골격 + fruto 관찰값 대체 (로그인/회원가입/응답자목록/데이터통계 4화면 근거) | Step 2 | 02-design-system-builder |
