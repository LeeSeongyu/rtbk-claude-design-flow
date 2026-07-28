# RTBK Design System — Figma 파일

디자인 시스템의 Figma 사본. 정본 문서는 `.claude/skills/design-system/SKILL.md`, 관찰값은
`fruto-visual-extraction.md`. Figma에는 변수·텍스트 스타일·컴포넌트로 구현.

- **URL**: https://www.figma.com/design/4MilB22X17pyPF4WE0Iyn6/RTBK-Design-System
- **file_key**: `4MilB22X17pyPF4WE0Iyn6`
- **팀**: DD
- **구성 (v2 — Carbon 전 컴포넌트 보강 중)**:
  - Variables — `Primitives` 44(색/간격/반경), `Color` **77 Semantic**(Carbon 그룹 미러링:
    Background/Layer/Field/Border/Text/Icon/Link/Button/Support/Focus/Notification/Status/Tag/Misc,
    Primitives에 alias, scope·`var(--…)` 코드 syntax)
  - Text styles 6 (Inter, Pretendard 확정 예정), Effect styles 3 (shadow-sm/md/lg)
  - **Foundation 페이지**: 🎨 Color(77 스와치) · 🔠 Typography · 📏 Spacing · 🌑 Effects · 🔲 Grid
  - **Component 페이지(각 1개, fruto 스타일)**: Button · Checkbox · Radio button · Toggle ·
    Text input · Password input · Search · Dropdown · Tag(+Badge) · Notification · Pagination ·
    Tabs · Breadcrumb · Data table · Modal · Progress bar · UI shell - Header
  - **남은 Carbon 컴포넌트(진행 예정)**: Accordion, Code snippet, Contained list, Content switcher,
    Date picker, File uploader, Form, Link, List, Loading, Menu, Menu buttons, Number input, Popover,
    Progress indicator, Select, Slider, Structured list, Text area, Tile, Toggletip, Tooltip, Tree view,
    UI shell - Left/Right panel (AI 계열은 범위 외로 보류)

> 방식: **Carbon v11 카탈로그를 다 fruto 스타일로 재정의**, RTBK 불필요분은 화면 제작 시 정리.
> 값은 fruto 관찰 기반 임시치(정밀 hex/폰트 확정 예정). 살아있는 문서.
