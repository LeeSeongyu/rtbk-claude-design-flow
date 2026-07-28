---
name: design-system
description: RTBK Design System — 모든 화면에 공통 적용되는 비주얼 토큰과 컴포넌트 상태 규칙. 값의 출처는 fruto Figma, 문서의 형식·구조는 Carbon Design System v11 양식. 화면을 만들며 계속 확장되는 살아있는 문서. 02-design-system-builder가 owner, 03~06이 참조.
---

# RTBK Design System

RTBK의 모든 화면이 따르는 **비주얼 토큰과 컴포넌트 상태 규칙(HOW)**을 정의하는 살아있는 문서입니다.

> **두 개의 출처**
> - **값(색·타이포·간격·컴포넌트 룩)** ← fruto Figma 파일 (`data/00-inputs/fruto-design/fruto-source.md`)
> - **형식·구조·토큰 네이밍·컴포넌트 분류·상태 체계** ← Carbon Design System v11 양식 (`data/00-inputs/carbon-format/`)
>
> 즉 **fruto 값 × Carbon v11 형식 = RTBK Design System.** 값은 fruto, 짜임새는 Carbon v11.

> **관심사 분리** — 이 파일은 "컴포넌트가 어떻게 생기고 동작하는가(HOW)". "어떤 화면·흐름을
> 거치는가(WHAT)"는 화면 정의/브리프가 담는다. "버튼 hover 색상"은 여기에 적는다.

## 살아있는 문서 (Living)

- 이 시스템은 **한 번에 완성되지 않는다.** 화면을 만들며(Step 3~6) 새 컴포넌트·토큰이 필요하면
  **여기에 추가되며 계속 갱신**된다.
- 추가·변경의 owner는 `02-design-system-builder`다. 다른 에이전트(03/05/06)는 필요한 새 요소를
  `data/02-design-system/needed-additions.md`에 기록하고 추가를 요청한다 — **직접 스타일을 지어내지 않는다.**
- 모든 추가·변경은 아래 **변경 로그**에 남긴다.

## 값의 규칙 (출처 표기)

- 각 값/행 끝에 `[출처]`를 표기: `추출(fruto)` · `확정(사람)` · `미확인`(fruto에 없어 미정).
- **원시 hex/px를 근거 없이 박지 않는다.** `미확인`은 `미확인`으로 남기고 사람이 확정한다.
- 형식(카테고리·네이밍·상태 체계)은 Carbon v11 양식을 따르되, 실제 값은 fruto에서 온다.

```
component-rules-verified: false   # fruto 추출·확정이 끝나 미확인이 없으면 true
```

---

# 아래 구조는 Carbon v11 양식에 맞춰 채운다 (값은 fruto 추출)

> `02-design-system-builder`가 `data/00-inputs/carbon-format/`의 실제 양식을 읽어 이 골격을
> 확정·조정한다. 아래는 Carbon v11의 일반적 조직을 반영한 뼈대이며, 값은 모두 fruto에서 채운다.

## 1. 색상 토큰 (Color)

> Carbon식 역할 기반 토큰(예: background / layer / field / border / text / interactive / support).
> 각 역할 토큰의 값은 fruto 팔레트에서 매핑한다.

| 역할 토큰 | 값(fruto) | 출처 |
|---|---|---|
| `$background` | (미추출) | 미확인 |
| `$layer` | (미추출) | 미확인 |
| `$field` | (미추출) | 미확인 |
| `$border-subtle` | (미추출) | 미확인 |
| `$text-primary` | (미추출) | 미확인 |
| `$text-secondary` | (미추출) | 미확인 |
| `$interactive` (primary) | (미추출) | 미확인 |
| `$support-error/success/warning` | (미추출) | 미확인 |

## 2. 타이포그래피 (Type)

> Carbon식 타입 세트(예: body-01, heading-01…). 폰트·사이즈·weight·line-height는 fruto에서.

| 타입 세트 | 폰트/사이즈/weight/lh | 출처 |
|---|---|---|
| `body-01` | (미추출) | 미확인 |
| `heading-01` | (미추출) | 미확인 |
| `display-01` | (미추출) | 미확인 |

## 3. 스페이싱 (Spacing)

> Carbon식 스페이싱 스케일(예: spacing-01 … spacing-13). 값은 fruto 간격 체계에서.

| 스텝 | 값(fruto) | 출처 |
|---|---|---|
| `spacing-01` … `spacing-13` | (미추출) | 미확인 |

## 4. 기타 토큰

| 토큰 | 값(fruto) | 출처 |
|---|---|---|
| radius (sm/md/lg) | (미추출) | 미확인 |
| motion (fast/moderate + easing) | (미추출) | 미확인 |
| elevation/shadow | (미추출) | 미확인 |

## 5. 컴포넌트 상태 규칙

> Carbon식 컴포넌트별 variant·state 구조로 정리. 값은 위 토큰 참조(= fruto).

### Button (variant: primary/secondary/ghost/danger …)
| state | 스타일(토큰 참조) | 출처 |
|---|---|---|
| enabled | (채움) | 미확인 |
| hover | (채움) | 미확인 |
| focus | (채움) | 미확인 |
| active | (채움) | 미확인 |
| disabled | (채움) | 미확인 |

### Input / Field
| state | 스타일 | 출처 |
|---|---|---|
| enabled / focus / error / disabled | (채움) | 미확인 |

### (이후 화면을 만들며 필요한 컴포넌트를 여기에 추가)

## 6. 반응형 / 접근성

- Carbon 2x Grid 원칙 참고, mobile-first, 상대 단위. 터치 타겟 최소 44×44px.
- 대비·포커스 표시·시맨틱 마크업 기본 준수.

---

## 사용 규칙

- **`02-design-system-builder`** — 이 파일의 owner. fruto 추출 + Carbon v11 형식으로 채우고 확장한다.
- **`03-screen-designer`** — 비주얼은 여기 참조. 없는 컴포넌트는 `needed-additions.md`에 기록.
- **`05-figma-builder`** — Figma 빌드 시 여기 토큰/변수 사용. 없는 값 신규 생성 금지(DS에 먼저 추가).
- **`06-coder`** — Tailwind 토큰을 여기 토큰과 매핑. 임의 hex/px 금지.

## 변경 로그 (Living)

| 날짜 | 변경 | 출처/사유 | 담당 |
|---|---|---|---|
| (초기) | 골격 생성 (Carbon v11 형식, fruto 값 대기) | Step 2 | 02-design-system-builder |
