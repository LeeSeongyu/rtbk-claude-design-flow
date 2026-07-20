<!--
사람이 작성하는 레퍼런스 문서 템플릿입니다.
사용법: 이 파일을 case-N/case-N.md 로 복사한 뒤 내용을 채우세요.
  예) cp data/01-references/_TEMPLATE-case.md data/01-references/case-1/case-1.md

원칙:
- 이 문서는 "어떤 화면 흐름을 거치는가(WHAT)"만 담습니다.
- "컴포넌트가 어떻게 보이는가(hover 색상, focus ring, disabled 스타일 등, HOW)"는
  여기 적지 말고 design-system 스킬(.claude/skills/design-system/SKILL.md)이 담당합니다.
  예) "Edit 클릭 → 편집 모드 전환"까지만 적고, 편집 인풋의 border/focus는 적지 않습니다.
-->

# Reference Case: {case-name}

## 출처
- 서비스명 / 캡처 일자 / 스크린샷 경로

## 사용자 시나리오 (Task Flow)

| 순서 | 트리거 (어디를 어떻게) | 결과 (화면/상태 변화) | 스크린샷 |
|---|---|---|---|
| 1 | 좌측 사이드바 "To review" 클릭 | 리스트가 필터링됨 | 01.png |
| 2 | 리스트에서 문서 행 클릭 | 우측 상세 패널 로드 | 02.png |
| 3 | "Edit" 버튼 클릭 | 편집 모드 전환 | 03.png |
| 4 | 값 수정 후 "Save" 클릭 | 저장 완료, 읽기 모드 복귀 | 04.png |

## 핵심 기능 Description
- 기능명 / 해결하는 문제 / 우리 서비스와 다른 점

## 신뢰도
각 항목별로 근거의 확실성을 표시: High / Medium / Low
- 스크린샷에 명확히 드러난 UI 요소 기반 → High
- 화면에 없는 동작·데이터·전후 맥락을 추론한 부분 → Medium 또는 Low
