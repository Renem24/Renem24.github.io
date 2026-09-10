# Plan 캘린더 설계 (2026-09-10)

## 목적
주간·월간 계획을 간단한 항목으로 적고, 깔끔한 캘린더로 블로그(renem24.github.io)에 남긴다.
브라우저에서 바로 입력하는 편의와 "블로그에 기록"을 둘 다 만족시킨다.

## 파일 구성 (기존 tools/playground 패턴)
- `quartz/static/plan/plan.html` — 캘린더 전체(단일 HTML, 외부 의존성 없음).
- `quartz/static/plan/plan.json` — 공개 계획 데이터(원본).
- `content/plan/index.md` — 사이드바 "Plan" 섹션. iframe 임베드 + 새 탭 링크.

## 데이터 형식 (`plan.json`)
```json
{
  "categories": [
    {"id": "research", "name": "연구", "color": "#2f6fed"},
    {"id": "invest",   "name": "투자", "color": "#dc3f36"},
    {"id": "personal", "name": "개인", "color": "#2a9d5c"}
  ],
  "items": [
    {"id": "a1b2", "date": "2026-09-15", "title": "논문 초안", "cat": "research", "done": false}
  ]
}
```
- 항목 필드는 `id, date(YYYY-MM-DD), title, cat, done` 다섯 개뿐. 시간·메모 없음.
- 카테고리는 JSON에서 정의(코드 수정 없이 추가 가능). 알 수 없는 `cat`은 회색으로 표시.

## 저장 흐름
1. 페이지 로드 시 `plan.json`(fetch, same-origin) → 기본 데이터.
2. localStorage 키 `plan.v1`에 로컬 편집본을 통째로 저장(항목 배열 + 카테고리). 로컬본이 있으면 그것을 표시, 없으면 리포지토리본을 표시.
3. 로컬본과 리포지토리본이 다르면 상단에 "미반영 변경 N건" 배지(추가/수정/삭제 항목 수).
4. 버튼: **JSON 내보내기**(현재 표시 데이터를 `plan.json`으로 다운로드) / **가져오기**(파일 선택 → 로컬본 교체) / **리포지토리 버전으로 되돌리기**(로컬본 삭제, 확인창).
5. 게시 절차: 내보낸 파일을 `quartz/static/plan/plan.json`에 덮어쓰고 `v5`에 push.

## UI
- 헤더: ‹ 이전 / 월 제목(YYYY년 M월) / 다음 › , "오늘" 버튼, 월간·주간 토글, 범례(카테고리 칩, 클릭 시 필터 토글), 변경 배지, 내보내기·가져오기·되돌리기.
- 월간 그리드: 7열(월요일 시작), 다른 달 날짜는 흐리게, 오늘 강조. 칸 안에 항목 칩(카테고리 색 점 + 제목, 완료 시 취소선·흐림). 칸 클릭(빈 곳) → 인라인 입력창(제목 + 카테고리 select, Enter 저장, Esc 취소).
- 주간 뷰: 해당 주 7일을 세로 목록으로. 각 날짜 행에 항목 목록 + "추가" 입력. 이전/다음이 주 단위로 이동.
- 항목 조작: 클릭 → 완료 토글, 호버 시 × → 삭제, 더블클릭 → 제목 편집.
- 스타일: 기존 `2026-08-investment-calendar.html`의 토큰(라이트/다크, `prefers-color-scheme` + `data-theme`) 재사용. 한국어 UI, `lang="ko"`.
- 뷰 상태(현재 월/주, 뷰 모드, 필터)는 localStorage `plan.ui`에 기억.

## 공개 범위
블로그는 공개. `plan.json`의 내용은 누구나 볼 수 있음. 비공개 항목은 로컬에만 두면 됨(내보내기 전에 삭제).

## 오류 처리
- `plan.json` fetch 실패(오프라인/404) → 빈 기본 데이터로 시작하고 상단에 안내 문구.
- localStorage 접근 예외 → try/catch, 메모리에서만 동작하고 안내 문구.
- 가져오기 파일이 형식에 맞지 않으면 거부하고 메시지.

## 검증
1. `source ~/.nvm/nvm.sh && nvm use 24.11.1 && npx quartz build` 성공, `public/static/plan/plan.html`·`plan.json`·`public/plan/index.html` 생성 확인.
2. 브라우저(로컬 서버)에서: 월간↔주간 전환, 이전/다음/오늘, 추가·완료·삭제·편집, 배지 카운트, 내보내기 파일 형식, 가져오기, 되돌리기, 새로고침 후 유지, 라이트/다크.
3. `v5` push 후 실제 사이트에서 iframe·새 탭 링크 동작 확인.

## 범위 밖
자동 동기화(외부 백엔드), 반복 일정, 시간대, 알림, 드래그 이동.
