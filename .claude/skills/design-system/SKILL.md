---
name: design-system
description: 코어 UI의 디자인 시스템. 모든 화면에 공통 적용되는 토큰, 컴포넌트 상태별 스타일·인터랙션, 타이포그래피, 반응형 규칙을 정의한다. 02-coder(코드 구현)와 01-case-deriver(케이스 도출)가 공통으로 참조한다.
---

# <제품명> Design System

`data/00-core-ui/`에 수집된 코어 UI 구조 데이터와 디자인 변수(토큰)를 근거로,
**모든 화면이 따르는 컴포넌트 스타일과 상태별 인터랙션을 한 번 정의**하는 스킬입니다.

> 관심사 분리:
> - **이 파일(HOW)** — 컴포넌트가 *어떻게 생기고 동작하는가*. 예: 버튼 hover → `--color-primary-dark`, `transition-fast`.
> - **`case-N.md`(WHAT)** — 사용자가 *어떤 화면 흐름을 거치는가*. 예: "Edit 클릭 → 편집 모드 전환".
>
> "Edit 버튼의 hover 색상"은 `case-N.md`가 아니라 **여기**에 적는다.

## 값의 출처 (중요)

- 아래 표의 스타일 값은 **토큰 *이름* 참조**다(`--color-primary`, `radius-md`, `transition-fast` 등).
  실제 hex/px 값은 **토큰 섹션**에서 정의하며, 그 값은 `00-figma-fetcher`가 수집한
  `data/00-core-ui/`의 디자인 변수에서 가져온다. **스킬에 원시 hex/px를 직접 박지 않는다.**
- 참조한 토큰이 아직 토큰 섹션에 없으면 → 그것은 **채워야 할 플레이스홀더**이지,
  임의로 지어낸 값이 아니다.
- 아래 **컴포넌트 상태 표는 코어 UI 수집 전까지 "초기 기본값(초안)"**이다.
  `data/00-core-ui/` 수집 후 실제 값·상태로 반드시 조정한다. 미검증 값을 확정 규칙처럼 취급하지 않는다.

## 토큰

> `00-figma-fetcher` 실행 후 `data/00-core-ui/`의 변수값으로 채운다. 미수집이면 먼저 fetcher를 실행한다.

- **색상**: `--color-primary`, `--color-primary-dark`, `--color-primary-light`, `--color-surface`,
  `--color-text`, `--color-text-secondary`, `--color-border`,
  의미색 스텝(`--color-gray-50`, `--color-blue-50`, `--color-red-500`, `--color-green-500` …)
- **스페이싱**: `--space-1` ~ `--space-8`
- **반경**: `--radius-sm`, `--radius-md`, `--radius-lg`
- **트랜지션**: `--transition-fast`(≈150ms ease), `--transition-normal`(≈200ms ease-out)

| 토큰 | 값 | 출처(Figma 변수명) |
|---|---|---|
| `--color-primary` | (미수집) | - |
| `--color-primary-dark` | (미수집) | - |
| `--radius-md` | (미수집) | - |
| `--transition-fast` | (미수집) | - |

## 컴포넌트 상태 규칙 (전역 — 모든 화면 공통)

> 값은 토큰 이름 참조. 아래는 코어 UI 수집 전 **초기 기본값**이며 수집 후 조정한다.

### 버튼
| 상태 | 스타일 |
|---|---|
| default | bg `--color-primary`, text white, `--radius-md` |
| hover | bg `--color-primary-dark`, `--transition-fast` |
| active | scale 0.98 |
| focus | ring-2 `--color-primary-light` |
| disabled | opacity 0.5, cursor not-allowed |
| loading | 텍스트 숨김, 중앙 spinner 표시 |

### 인풋 필드
| 상태 | 스타일 |
|---|---|
| default | border `--color-border`, bg white |
| focus | border `--color-primary`, ring-2 `--color-primary-light` |
| error | border `--color-red-500`, 하단에 에러 메시지 |
| disabled | bg `--color-gray-50`, text `--color-text-secondary` |
| read-only → edit 전환 | border 없는 텍스트 → border 있는 인풋으로, `--transition-normal` |

### 테이블/리스트 행
| 상태 | 스타일 |
|---|---|
| default | bg white |
| hover | bg `--color-gray-50`, cursor pointer |
| selected | 좌측 border-4 `--color-primary`, bg `--color-blue-50` |
| checkbox checked | 체크 표시 + 상단 배치 액션 버튼 활성화 |

### 모달/다이얼로그
| 상태 | 스타일 |
|---|---|
| 진입 | backdrop fade-in `--transition-normal`, 모달 scale 0.95→1.0 + fade-in |
| 퇴장 | 진입의 역순 |

### 토스트/알림
| 상태 | 스타일 |
|---|---|
| 성공 | bg `--color-green-50`, border `--color-green-500`, 체크 아이콘 |
| 에러 | bg `--color-red-50`, border `--color-red-500`, 경고 아이콘 |
| 자동 dismiss | 3초 후 fade-out |

## 타이포그래피

> 폰트·사이즈·weight는 코어 UI 수집값으로 채운다. line-height는 본문 최소 1.5를 지킨다.

- **Display**: (폰트, 사이즈, weight)
- **Body**: (폰트, 사이즈, line-height ≥ 1.5)
- **Caption**: (폰트, 사이즈)

## 반응형

- Mobile-first, 상대 단위·유연한 레이아웃 사용.
- 터치 타겟 **최소 44×44px**.

## 접근성 기본값

- 대비, 포커스 표시, 시맨틱 마크업을 기본으로 지킨다.

## 이 파일의 사용 규칙

- **`02-coder`** — 코드 작성 **전에 이 파일을 먼저 읽고**, 여기 정의된 토큰과 상태 규칙을 따른다.
  여기에 없는 임의 hex/px 값을 쓰지 않는다(불가피하면 근거를 주석으로 남긴다).
- **`01-case-deriver` / `case-N.md` 작성자** — `case-N.md`에 컴포넌트 스타일·인터랙션을
  **중복 기술하지 않는다.** `case-N.md`는 "어떤 화면 흐름을 거치는가"만 담고,
  "컴포넌트가 어떻게 보이는가"는 이 파일을 참조한다.
- **새 컴포넌트** — 여기에 먼저 추가한 뒤 사용한다.
  `case-N.md`나 코드에서 먼저 만들고 나중에 여기 반영하는 순서는 금지.

## 산출 기준 (체크리스트)

- [ ] 색상/간격/타이포가 토큰으로 참조되는가 (원시 hex/px 없음)?
- [ ] 컴포넌트 상태(hover/focus/active/disabled 등)가 이 파일 규칙과 일치하는가?
- [ ] 반복 UI가 컴포넌트로 분리됐는가?
- [ ] 레퍼런스의 구조·패턴·배치와 일치하는가?

## 비고

- 이 스킬은 **픽셀 단위 복제**가 목표가 아니다. 구조·패턴·토큰 일관성을 지향한다.
- 채점 기준은 `visual-verdict` 스킬과 정렬되어 있다.
