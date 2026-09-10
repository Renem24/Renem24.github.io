# Plan 캘린더 Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** 주간·월간 계획 항목을 브라우저에서 입력하고 캘린더로 보여주는 단일 HTML 도구를 블로그의 Plan 섹션으로 배포한다.

**Architecture:** `quartz/static/plan/plan.html` 하나에 UI·저장 로직을 담고, `plan.json`을 fetch해 기본 데이터로 쓴다. 브라우저 편집은 localStorage에 덮어쓰고, 내보내기로 JSON을 받아 리포지토리에 반영한다. `content/plan/index.md`가 iframe으로 임베드한다.

**Tech Stack:** 순수 HTML/CSS/JS(의존성 없음), Quartz v5 정적 빌드(node 24), GitHub Pages(`v5` 브랜치 push).

**Spec:** `docs/superpowers/specs/2026-09-10-plan-calendar-design.md`

## Global Constraints
- 외부 라이브러리·CDN 없음. 단일 HTML 파일.
- `lang="ko"`, 한국어 UI. 라이트/다크: `prefers-color-scheme` + `:root[data-theme]` 둘 다 지원.
- 항목 필드는 `id, date, title, cat, done` 다섯 개만.
- localStorage 키: 데이터 `plan.v1`, UI 상태 `plan.ui`. 모든 접근은 try/catch.
- 빌드: `source ~/.nvm/nvm.sh && nvm use 24.11.1 && npx quartz build`.

---

### Task 1: 데이터 파일과 로직 뼈대

**Files:**
- Create: `quartz/static/plan/plan.json`
- Create: `quartz/static/plan/plan.html` (스타일 토큰 + 로직만, UI는 Task 2)

**Interfaces (Produces):**
- `loadRepo(): Promise<PlanData|null>` — fetch `plan.json`; 실패 시 null.
- `loadLocal(): PlanData|null`, `saveLocal(data)`, `clearLocal()`.
- `diffCount(repo, local): number` — 추가+수정+삭제 항목 수.
- `PlanData = {categories:[{id,name,color}], items:[{id,date,title,cat,done}]}`.
- `validate(obj): PlanData|null` — 가져오기 검증.

- [ ] **Step 1:** `plan.json` 작성 (연구/투자/개인 3개 카테고리, 샘플 항목 2개).
- [ ] **Step 2:** `plan.html` 문서 뼈대 + `2026-08-investment-calendar.html`의 색 토큰 복사 + 위 함수 구현.
- [ ] **Step 3:** 브라우저 콘솔에서 `diffCount`·`validate` 수동 확인 (잘못된 객체 → null, 항목 하나 추가 → 1).
- [ ] **Step 4:** Commit `feat(plan): 데이터 파일과 저장 로직`.

### Task 2: 월간 그리드 + 항목 조작

**Files:**
- Modify: `quartz/static/plan/plan.html`

**Interfaces (Produces):** `render()` — 상태(`state.view`, `state.cursor`(Date), `state.filter`(Set<catId>))로 화면 전체를 다시 그림. `addItem(date,title,cat)`, `toggleDone(id)`, `removeItem(id)`, `renameItem(id,title)` 은 모두 `saveLocal` 후 `render()`.

- [ ] **Step 1:** 헤더(이전/다음/오늘/월 제목/범례/버튼 자리) 마크업과 월간 7열 그리드 렌더(월요일 시작, 다른 달 흐림, 오늘 강조).
- [ ] **Step 2:** 항목 칩 렌더(카테고리 색 점, 완료 시 취소선), 칩 클릭 완료 토글, × 삭제, 더블클릭 이름 편집(prompt 대신 인라인 input).
- [ ] **Step 3:** 빈 칸 클릭 → 인라인 입력창(제목 input + 카테고리 select, Enter 저장, Esc 취소).
- [ ] **Step 4:** 범례 칩 클릭 필터 토글, UI 상태 `plan.ui` 저장/복원.
- [ ] **Step 5:** 브라우저에서 추가·완료·삭제·편집·새로고침 유지 확인. Commit `feat(plan): 월간 캘린더와 항목 편집`.

### Task 3: 주간 뷰 + 저장 흐름 버튼

**Files:**
- Modify: `quartz/static/plan/plan.html`

- [ ] **Step 1:** 월간/주간 토글. 주간: 커서가 속한 주(월~일) 7행 세로 목록, 행마다 항목 + 추가 입력. 이전/다음이 주 단위 이동.
- [ ] **Step 2:** 변경 배지(`diffCount`>0일 때 "미반영 변경 N건"), 내보내기(현재 데이터를 `plan.json` 이름으로 다운로드, 들여쓰기 2), 가져오기(`<input type=file>` → `validate` → `saveLocal`), 되돌리기(`confirm` 후 `clearLocal`).
- [ ] **Step 3:** fetch 실패·localStorage 예외 시 상단 안내 문구.
- [ ] **Step 4:** 브라우저 확인 후 Commit `feat(plan): 주간 뷰와 JSON 내보내기/가져오기`.

### Task 4: 블로그 섹션 연결과 배포

**Files:**
- Create: `content/plan/index.md`

- [ ] **Step 1:** `content/tools/index.md` 형식으로 Plan 섹션 작성: 설명, 사용법(브라우저 입력 → 내보내기 → `quartz/static/plan/plan.json` 교체 → push), iframe(`/static/plan/plan.html`, height 900px), 새 탭 링크.
- [ ] **Step 2:** `npx quartz build` 성공, `public/static/plan/plan.html`, `public/static/plan/plan.json`, `public/plan/index.html` 존재 확인.
- [ ] **Step 3:** `npx quartz build --serve`로 `/plan` 페이지에서 iframe 동작·다크 모드 확인.
- [ ] **Step 4:** Commit `feat: Plan 섹션 추가 — 주간·월간 계획 캘린더`, `git push origin v5`, 사이트에서 확인.
