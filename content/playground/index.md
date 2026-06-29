---
title: Playground
---

외부 라이브러리·이미지·네트워크 의존성 없이, 순수 JavaScript 소프트웨어 래스터라이저로 동작하는 ASCII 아트 데모 모음입니다. 각 데모는 단일 HTML 파일이며 브라우저에서 바로 실행됩니다.

## 🍩 회전하는 ASCII 3D 도형

z-버퍼 + 램버트 음영으로 도넛 / 정육면체 / 구를 문자 농담(`.,-~:;=!*#$@`)으로 렌더링합니다. 도형·색상 전환, 회전 속도 조절, CRT 주사선 효과를 지원합니다.

<iframe src="/static/playground/ascii-3d.html" title="ASCII 3D" loading="lazy"
        style="width:100%;max-width:800px;height:760px;border:0;border-radius:10px;display:block;margin:0 auto;background:#0c0a06;"></iframe>

<a href="/static/playground/ascii-3d.html" target="_blank" rel="noopener">↗ 새 탭에서 전체 화면으로 열기</a>

## 🪐 ASCII 태양계

광선-구 교차로 천체를 채우고 깊이 버퍼로 가림 처리한 컬러 ASCII 3D 태양계입니다. 드래그로 시점 회전, 휠로 확대, 행성 클릭 시 추적 + 정보 패널이 표시됩니다.

<iframe src="/static/playground/solar-ascii.html" title="ASCII 태양계" loading="lazy"
        style="width:100%;height:620px;border:0;border-radius:10px;display:block;background:#04060d;"></iframe>

<a href="/static/playground/solar-ascii.html" target="_blank" rel="noopener">↗ 새 탭에서 전체 화면으로 열기</a>

## 🌊 ASCII 유체 시뮬레이션

안정 유체(이류 + 압력 투영 + 와도 보존 + 부력) 솔버를 매 프레임 돌려 만든 실시간 연기입니다. 화면을 드래그하면 속도장이 따라 휘어 연기가 빨려 들어가고, 부력·소용돌이 세기와 인광 색을 조절할 수 있습니다.

<iframe src="/static/playground/fluid-ascii.html" title="ASCII 유체" loading="lazy"
        style="width:100%;max-width:800px;height:840px;border:0;border-radius:10px;display:block;margin:0 auto;background:#060a0c;"></iframe>

<a href="/static/playground/fluid-ascii.html" target="_blank" rel="noopener">↗ 새 탭에서 전체 화면으로 열기</a>

## ⏳ 떨어지는 모래

모래·물·벽·식물·불을 칠해 넣으면 셀 자동자 규칙으로 상호작용하는 픽셀 샌드박스입니다. 모래는 물에 가라앉고, 물은 빈 곳으로 퍼지며, 불은 식물을 태우고 물에 닿으면 연기로 꺼지고, 식물은 물을 따라 자랍니다. 색이 입혀진 ASCII 글리프를 캔버스에 직접 찍어 렌더링합니다.

<iframe src="/static/playground/sand-ascii.html" title="떨어지는 모래" loading="lazy"
        style="width:100%;max-width:800px;height:940px;border:0;border-radius:10px;display:block;margin:0 auto;background:#0a0b0e;"></iframe>

<a href="/static/playground/sand-ascii.html" target="_blank" rel="noopener">↗ 새 탭에서 전체 화면으로 열기</a>
