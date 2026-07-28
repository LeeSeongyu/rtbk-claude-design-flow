# fruto 비주얼 추출 (관찰 기반)

> fruto Figma에는 변수/스타일이 없어 **화면을 눈으로 읽어** 값을 관찰했다. 아래 값은 스크린샷 관찰
> 기반의 **근사치(추정)**이며, 정확한 hex/폰트/치수는 후속 확정 필요(사람 또는 특정 노드 `get_design_context`).
> 파일: `YZOL3M3D0aOnz7rLjhMkwJ` (Fruto). fruto는 상담/자가진단 제품 — RTBK와 주제는 무관, **비주얼만** 차용.

## 근거 화면 (읽은 노드)

| 노드ID | 화면 | 얻은 요소 |
|---|---|---|
| 3:82108 | 로그인 | 배경, 로고, primary 버튼, 텍스트 인풋, password 인풋, 체크박스, 링크, 푸터 |
| 3:78602 | 회원가입 > 회원 정보 입력 | 스텝퍼(1–5), 상단 뒤로가기, 인풋(gray fill), segmented(남/여), **disabled 버튼** |
| 10:78542 | 자가진단 응답자 목록 | **앱셸(상단 GNB)**, 2차 탭, 탭(밑줄), 페이지헤더, **Tag(D-19)**, 데이터테이블, **status(색점+텍스트)**, 필터 드롭다운, 검색, 아이콘버튼, **날짜 레인지 피커** |
| 10:72365 | 상담 데이터/통계 현황 | 퀵레인지 칩, 바차트+범례, **stat 테이블(라이트 헤더/합계행)**, 탭(active 인디고) |

## 색상 (관찰·추정)

| 역할 | 값(추정) | 근거 |
|---|---|---|
| 브랜드 Primary (인디고) | `#5A5CE0` 계열 | 로그인 버튼, active 네비/탭, D-19 배지, 캘린더 오늘, 차트 주색 |
| Primary hover(진한) | `#4A4CD0` 계열(추정) | (관찰 안 됨, 추정) |
| Text primary (딥네이비) | `#22242F` 계열 | 제목/본문 |
| Text secondary (회색) | `#6B7280` 계열 | 라벨·보조 텍스트 |
| Placeholder/disabled text | `#A0A3B1` 계열 | 인풋 플레이스홀더, disabled 버튼 텍스트 |
| Border subtle | `#E9EAF0` 계열 | 인풋 보더, 테이블 구분선 |
| Field fill (기본) | `#F1F2F8`(회색) / 흰색 | 회원정보 인풋=회색fill, 로그인 인풋=흰색 |
| Page background | `#EEF0FA`(라이트 라벤더) | 인증 화면 배경 |
| Surface/Layer | `#FFFFFF` | 콘텐츠 영역 |
| Table header fill | `#EEEFF9`(라이트 라벤더) | stat 테이블 헤더/합계행 |
| Support success (정상) | `#22C55E` 계열(녹색) | status 점 |
| Support warning (경고) | `#EAB308`/`#F5A623`(앰버) | status 점 |
| Support error (위험) | `#EF4444` 계열(빨강) | status 점 |
| Chart categorical | 인디고·앰버·코랄·그린·퍼플·틸 | 바차트 범례(학부/대학원/연구원/행정/직원/교원) |

## 타이포그래피 (관찰·추정)

- **폰트**: 한글 산세리프 — Pretendard 계열로 추정. **확인 필요(미확인).**
- **weight**: Bold(제목), Medium(라벨·버튼·active 네비), Regular(본문)
- **스케일(1280 화면 기준 근사)**: 페이지 타이틀 ~24–28 Bold / 섹션·카드 타이틀 ~18–20 / 본문 ~14–15 / 캡션·메타 ~12–13 / 네비 ~15

## 형태 (관찰·추정)

- **Radius**: 인증 버튼·인풋 = 거의 pill(완전 둥금); 앱 내 요소는 ~12–16px 라운드; 칩 = pill; 카드/테이블 = ~8–12px. (혼재 — **값 확인 필요**)
- **버튼 높이**: ~52–56px(인증), 앱 내 컨트롤 ~36–40px
- **간격 리듬**: 8px 기반으로 보임 (Carbon 8px mini-unit과 정합)

## 관찰된 컴포넌트 (fruto) → Carbon 매핑 대상

앱셸(헤더/네비), 탭(밑줄), 2차 탭, 뒤로가기 링크, 페이지헤더+메타그리드, **Tag/Badge**(인디고 pill),
**Status**(색점+텍스트: 정상/경고/위험), **Data Table**(정렬헤더·행구분·zebra·합계행), **Dropdown 필터**(pill),
**Search**, **아이콘 버튼**, **Date Picker**(캘린더+퀵칩), **Overflow menu(…)**, **Button**(primary/ disabled),
**Text Input**(기본/gray fill/password+reveal), **Checkbox**(원형 체크 — Carbon과 형태 상이), **Segmented/Content switcher**(남/여),
**Progress Indicator/Stepper**(1–5), **퀵레인지 칩**(toggle), **Bar chart+범례**, **Stat 테이블**.

## 미확인 / 확정 필요

- 정확한 hex 값 전부 (관찰 추정치) — 특정 컴포넌트 노드 `get_design_context`로 정밀 추출 또는 사람 확정
- 폰트 패밀리(Pretendard? 확인)
- Radius 정확값, 컨트롤 높이, 간격 스케일 수치
- hover/focus/pressed 등 인터랙션 상태 색 (정적 스크린샷에서 미관찰 → Carbon 기본 or 사람 확정)
