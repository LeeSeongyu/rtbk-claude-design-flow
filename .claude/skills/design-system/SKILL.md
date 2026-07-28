---
name: design-system
description: fruto Design System — 모든 화면에 공통 적용되는 비주얼 토큰과 컴포넌트 상태별 스타일·인터랙션을 한 번 정의한다. 비주얼 값의 출처는 사용자가 제공한 fruto Figma 파일. 02-screen-designer가 채우고, 04-figma-builder·05-coder가 참조한다.
---

# fruto Design System

**모든 화면이 따르는 비주얼 토큰과 컴포넌트 상태 규칙(HOW)을 한 번 정의**하는 스킬입니다.

> 관심사 분리:
> - **이 파일(HOW)** — 컴포넌트가 *어떻게 생기고 동작하는가*. 예: 버튼 hover → `--color-primary-dark`.
> - **화면 정의 / 브리프(WHAT)** — 사용자가 *어떤 화면·흐름을 거치는가*.
>
> "버튼의 hover 색상"은 화면 정의가 아니라 **여기**에 적는다.

## 비주얼의 출처 (중요)

- **fruto Design System의 비주얼 값(색·타이포·간격·반경·컴포넌트 룩)은 사용자가 제공한
  fruto Figma 파일에서 추출한다.** (`data/00-inputs/fruto-design/fruto-source.md`의 URL)
- 추출은 `02-screen-designer`가 Figma MCP(`get_variable_defs`, `get_design_context`)로 수행한다.
- **fruto에 없는 값을 임의로 지어내지 않는다.** 확인 불가한 값은 `미확인`으로 남기고
  사람이 확정한다. 원시 hex/px를 근거 없이 박지 않는다.
- UX·패턴(레이아웃 로직, 인터랙션 흐름)은 Mobbin/경쟁서비스 참고지만,
  **비주얼 값의 단일 출처는 fruto다.**

## 검증 상태 (component-rules-verified)

<!-- fruto 추출·확정이 끝나면 false → true. 05-coder는 이 값이 false면 중단하지 않지만,
     핵심 상태가 다수 '미확인'이면 사람에게 보완을 요청한다. -->

```
component-rules-verified: false
```

- **의미** — 아래 토큰·상태 규칙이 fruto 실제 값에 맞춰 채워졌는지 여부.
- **출처 표기** — 각 값/행 끝의 `[출처]`:
  `추출(fruto)`(Figma에서 확인) · `확정`(사람이 결정) · `미확인`(fruto에 없어 미정).
  `미확인`이 남아 있으면 플래그를 `true`로 두지 않는다.

## 토큰

> `02-screen-designer`가 fruto Figma에서 추출해 채운다. 미추출 상태면 Step 2를 먼저 실행한다.

| 토큰 | 값 | 출처 |
|---|---|---|
| `--color-primary` | (미추출) | 미확인 |
| `--color-primary-dark` | (미추출) | 미확인 |
| `--color-surface` | (미추출) | 미확인 |
| `--color-text` | (미추출) | 미확인 |
| `--color-border` | (미추출) | 미확인 |
| `--space-1` … `--space-8` | (미추출) | 미확인 |
| `--radius-sm/md/lg` | (미추출) | 미확인 |
| `--transition-fast` | (미추출) | 미확인 |

## 컴포넌트 상태 규칙 (전역 — 모든 화면 공통)

> 값은 토큰 이름 참조. fruto에서 추출한 값으로 채우고, 각 행 출처를 표기한다.

### 버튼
| 상태 | 스타일 | 출처 |
|---|---|---|
| default | (fruto에서 채움) | 미확인 |
| hover | (fruto에서 채움) | 미확인 |
| active | (fruto에서 채움) | 미확인 |
| focus | (fruto에서 채움) | 미확인 |
| disabled | (fruto에서 채움) | 미확인 |

### 인풋 필드
| 상태 | 스타일 | 출처 |
|---|---|---|
| default | (fruto에서 채움) | 미확인 |
| focus | (fruto에서 채움) | 미확인 |
| error | (fruto에서 채움) | 미확인 |
| disabled | (fruto에서 채움) | 미확인 |

### 리스트/카드
| 상태 | 스타일 | 출처 |
|---|---|---|
| default | (fruto에서 채움) | 미확인 |
| hover | (fruto에서 채움) | 미확인 |
| selected | (fruto에서 채움) | 미확인 |

### 모달 / 토스트
| 요소 | 스타일 | 출처 |
|---|---|---|
| 모달 진입/퇴장 | (fruto에서 채움) | 미확인 |
| 토스트 성공/에러 | (fruto에서 채움) | 미확인 |

## 타이포그래피

> fruto 추출값으로 채운다. line-height는 본문 최소 1.5.

- **Display / Heading / Body / Caption**: (폰트, 사이즈, weight, line-height) — 미추출

## 반응형 / 접근성

- Mobile-first, 상대 단위·유연한 레이아웃. 터치 타겟 최소 44×44px.
- 대비·포커스 표시·시맨틱 마크업 기본 준수.

## 이 파일의 사용 규칙

- **`04-figma-builder`** — Figma 빌드 시 여기 토큰/변수를 사용한다. fruto에 없는 값 신규 생성 금지.
- **`05-coder`** — 코드 작성 전 이 파일을 읽고 토큰·상태 규칙을 따른다.
  Tailwind 토큰을 fruto 토큰과 매핑하고, 임의 hex/px를 쓰지 않는다.
- **`03-brief-writer`** — 브리프에 비주얼 제약을 넣을 때 여기 토큰을 인용한다.
- **새 컴포넌트** — 여기에 먼저 추가한 뒤 사용한다.

## 산출 기준 (체크리스트)

- [ ] 비주얼 값이 fruto에서 추출됐고 출처가 표기됐는가 (임의 hex/px 없음)?
- [ ] 컴포넌트 상태(hover/focus/disabled 등)가 정의됐는가?
- [ ] `미확인`이 남았다면 사람 확정 대상으로 표시됐는가?

## 비고

- 이 스킬은 픽셀 복제가 목표가 아니라 **fruto 비주얼 + 레퍼런스 UX의 일관 적용**이 목표다.
