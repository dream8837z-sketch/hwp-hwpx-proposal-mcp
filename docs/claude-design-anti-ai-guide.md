# 클로드 디자인에서 "AI 느낌" 제거 가이드

> 대상: 한글 제안서(.hwp / .hwpx / 슬라이드 / HTML)를 Claude로 디자인할 때
> 목표: 문단 간격 틀어짐 · 템플릿 붕괴 · 도형(다이어그램) 오류 등 "AI가 만든 티"를 구조적으로 제거
> 참고: 폰트와 우수제안서 원본은 사용자가 직접 삽입 (본 문서는 그 외 모든 것을 다룸)

---

## 1. 왜 AI 결과물은 "AI처럼" 보이는가 (근본 원인)

웹 리서치와 실무 자료를 종합하면, AI 디자인의 어색함은 대부분 **세 가지 근본 원인**에서 나오며, 사용자가 지적한 증상과 정확히 대응됩니다.

| 사용자가 겪는 증상 | 근본 원인 | 왜 발생하나 |
|---|---|---|
| **문단 간격이 틀어짐** | 간격(spacing) 값을 매번 "새로 지어냄" | AI는 요소마다 margin/줄간격을 개별 추정 → 4pt, 6pt, 7pt, 10pt가 뒤섞여 리듬이 깨짐 |
| **템플릿 붕괴 / 슬라이드마다 다름** | 고정된 마스터/그리드가 없음 | 페이지를 매번 "처음부터" 생성 → 여백·정렬·머리말 위치가 페이지마다 드리프트(drift) |
| **도형·다이어그램 오류** | 좌표를 절대값으로 즉흥 계산 | 박스 겹침, 화살표 어긋남, 텍스트 오버플로 → 그리드/앵커 없이 x/y를 눈대중으로 찍기 때문 |

핵심 통찰(2Slides, Presenti.ai, Beautiful.ai 등 실무 블로그 공통):
- AI 결과물은 **"너무 일관되게 안전"**하거나(무채색·중간 톤 팔레트, 획일 레이아웃) 반대로 **"국소적으로 제멋대로"**(간격·좌표 즉흥 생성)인 양극단에 빠진다.
- 사람이 만든 문서는 **의도된 규칙(디자인 시스템) + 소수의 의도된 변주**를 가진다.
- 따라서 해법은 "AI에게 더 잘 그려달라고 부탁"이 아니라 **AI가 즉흥적으로 결정할 자유를 빼앗고, 검증 가능한 제약(constraint)을 주입**하는 것.

---

## 2. 핵심 해법: "생성"이 아니라 "채우기"로 전환

AI 느낌을 없애는 단 하나의 원칙:

> **Claude가 값을 발명(invent)하게 두지 말고, 미리 정의된 토큰·그리드·템플릿에서 값을 선택(select)하게 하라.**

이를 위한 4단 방어선(defense-in-depth):

1. **디자인 토큰 주입** — 간격·타이포·색상을 8pt 그리드 기반 유한 집합으로 고정 → 문단 간격 문제 원천 차단
   → `resources/krds-design-tokens.css`
2. **규칙(제약) 프롬프트 주입** — "빈 값이면 지어내지 말고 토큰에서 고르라"는 강제 규칙을 Claude에 입력
   → `resources/claude-design-rules.md`
3. **템플릿/마스터 채우기** — 처음부터 그리지 말고 검증된 .fig / HWPX / 슬라이드 마스터를 복제 후 내용만 교체
   → `resources/RESOURCES.md` (Figma .fig, KRDS 키트)
4. **생성 후 검증(lint)** — 결과물을 규칙에 맞는지 자동/수동 체크 → 도형 겹침·간격 이탈 잡아냄
   → 본 문서 §5 체크리스트

이 저장소의 HWP/HWPX 파이프라인(character width, letter spacing, margins, line spacing, font, bullet 규칙 강제)은 정확히 이 철학의 문서 버전입니다. 본 가이드는 그 앞단인 **"디자인/시각 레이어"**에 같은 원칙을 적용합니다.

---

## 3. 왜 KRDS를 기준으로 삼는가 (공신력)

한글 문서/제안서에서 "지어낸 값" 대신 쓸 **공신력 있는 기준값**이 필요합니다. 대한민국 정부가 공식 채택한 **KRDS(Korea Government Design System)**가 최적입니다.

- 대한민국 디지털 정부 서비스 **공식 디자인 시스템** (krds.go.kr)
- **Pretendard GOV** 표준 한글 폰트, **8pt 그리드**, 접근성(WCAG 2.1 AA) 검증된 색/타이포 토큰
- 정부·공공 제안서와 톤이 정확히 맞음 → "AI스러움" 대신 "공문서스러운 신뢰감"
- **오픈소스 + 무료 + 한글 네이티브** (MIT / OFL / KRDS 이용약관)

즉 KRDS 토큰을 Claude에 주입하면, Claude가 간격·글자크기·색을 **발명하지 않고 정부 표준값을 인용**하게 됩니다. 이것이 한글 문서에서 AI 느낌을 없애는 가장 빠른 지름길입니다.

---

## 3.5 실증 (Empirical Verification) — 이 방법이 실제로 작동하는가

말로만 "AI 느낌을 없앤다"가 아니라, 실제로 검증한 결과를 기록합니다.

**(1) KRDS MCP를 실제 호출해 값을 대조했더니, 손으로 추정한 값이 틀렸습니다.**
이 저장소 `.mcp.json`으로 연결한 `@krds-mcp/krds-mcp`(KRDS 2024 Complete v2.0.0, 토큰 350개)를
직접 조회한 결과, 초기 추정값을 다음과 같이 **정부 표준값으로 교정**했습니다:

| 항목 | 초기 추정(틀림) | KRDS 실측(정답) |
|---|---|---|
| 간격 스케일 | "8pt 그리드"(4·8·16·24·32…) | **4px 기반**(4·8·12·16·**20**·24·**28**·32·**36**…) |
| 주조색 Primary | `#256ef4` | **`#0F4C8C`** Government Blue (AAA) |
| 강조색 Point | `#f13636` | **`#CD2E3A`** Korean Red |
| 본문 텍스트 | `#1e2124` | **`#212529`** Gray 900 (AAA) |
| 본문 행간 | 1.6(추정) | **1.6**(확인) / 캡션 1.4·자간 0.025em |

→ 교훈: Claude가 색·간격을 **기억으로 지어내면 미묘하게 틀린다.** MCP로 표준값을 **조회**시키면
정확해진다. 이것이 §2 "발명 금지, 선택 강제" 원칙의 실증이다. 교정된 값은
`resources/krds-design-tokens.css`에 반영(출처·조회일 명시).

**(2) Before/After 실물 제안서 페이지로 차이를 눈으로 확인했습니다.**
같은 제안서 내용을 ① 전형적 "AI 느낌"(임의 간격 7·13px, 페이지마다 다른 여백, 도형 텍스트 넘침,
무채색 도피)과 ② KRDS 토큰 적용본으로 각각 렌더링해 비교했습니다.
→ `resources/demo/proposal-before-after.html` (브라우저로 열면 좌=Before, 우=After).
렌더 스크린샷도 동일 폴더에 첨부.

---

## 4. 실전 워크플로우 (Claude Design에 입력하는 순서)

```
[1] 폰트 설치            ← 사용자 직접 (Pretendard GOV)
[2] 우수제안서 원본 삽입  ← 사용자 직접 (레이아웃 레퍼런스로)
[3] 디자인 토큰 입력      → resources/krds-design-tokens.css 를 Claude에 첨부/붙여넣기
[4] 규칙 프롬프트 입력    → resources/claude-design-rules.md 를 시스템/스킬로 주입
[5] 템플릿(.fig) 복제     → RESOURCES.md의 KRDS Figma / 제안서 템플릿 duplicate
[6] "채우기" 지시        → "새 레이아웃을 만들지 말고 [4]규칙과 [3]토큰만 사용해 [2]구조를 채워라"
[7] 검증(lint)           → §5 체크리스트로 간격·도형·템플릿 이탈 점검
```

- HWPX 산출: 3~4번을 이 저장소의 `hwpx` 스킬 규칙과 결합 → 문단 간격/자간/여백이 토큰으로 잠김.
- 슬라이드/문서 산출: 5번의 .fig를 복제 → Claude에는 "값 생성 금지, 프레임 복제 후 텍스트만 교체" 지시.
- HTML/웹 산출: 3번 CSS를 그대로 링크 → KRDS-uiux 컴포넌트 붙여쓰기.

---

## 5. 생성 후 검증 체크리스트 (AI 느낌 lint)

Claude 결과물을 아래로 점검하세요. 하나라도 걸리면 "지어낸 값"이 남은 것입니다.

**문단/간격**
- [ ] 모든 세로 간격이 KRDS 스페이싱 스케일 값인가? (4px 기반: 4·8·12·16·20·24·28·32·36·40·48·64 … / 7·13px 같은 임의값 금지)
- [ ] 본문 줄간격(line-height)이 150~170%로 통일됐는가? (한글은 160% 권장)
- [ ] 같은 위계의 요소는 같은 간격을 쓰는가? (제목-본문 간격이 페이지마다 동일한가)
- [ ] 자간(letter-spacing)이 제목 -1~-2%, 본문 0으로 고정됐는가?

**템플릿/레이아웃**
- [ ] 모든 페이지의 상·하·좌·우 여백이 동일한가?
- [ ] 머리말/꼬리말/페이지번호 위치가 전 페이지 동일한가? (드리프트 없음)
- [ ] 좌우 정렬 기준선(그리드 컬럼)이 페이지 간 일치하는가?

**도형/다이어그램**
- [ ] 박스끼리 겹치거나 1~2px 어긋난 곳이 없는가?
- [ ] 화살표가 도형 앵커(중심/모서리)에 정확히 붙는가?
- [ ] 도형 안 텍스트가 넘치거나 잘리지 않는가?
- [ ] 도형 크기/색이 토큰(2~3색 팔레트)만 쓰는가? (무지개색 금지)

**전체 톤**
- [ ] 색이 무채색 회색으로 도망가지 않고 브랜드 1~2색을 확실히 쓰는가?
- [ ] 페이지 간 아이콘 스타일/이미지 톤이 통일됐는가?

---

## 6. 출처 (Sources)

**AI 느낌 원인·해법 (실무 자료)**
- [Why AI Presentations Look AI-Generated (And How to Fix It) — llemental](https://llemental.com/posts/why-ai-presentations-look-ai-generated)
- [How to Make Your AI Slides Look Less "AI-Generated" — Presenti.ai](https://presenti.ai/blog/humanize-ai-presentations/)
- [Why AI Slides Look Fake in 2026 (5 Fixes) — 2Slides](https://2slides.com/blog/why-ai-slides-look-fake-and-how-to-fix)
- [AI Can Build Slides Fast—But Great Presentations Still Need Design Rules — Beautiful.ai](https://www.beautiful.ai/blog/ai-can-build-slides-fast--but-great-presentations-still-need-design-rules)
- [7 Common Mistakes Using AI to Create Slides — smallppt](https://smallppt.com/blog/basics/common-ai-slide-mistakes-tips)

**공신력 있는 한글 디자인 표준 (KRDS)**
- [KRDS 공식 사이트](https://www.krds.go.kr/)
- [KRDS 서체(Typography) 스타일 가이드](https://v04.krds.go.kr/guide/style/style_03.html)
- [KRDS-MCP — AI에 KRDS 디자인 시스템을 주입하는 MCP 서버 (GitHub)](https://github.com/KRDS-MCP/krds-mcp)
- [KRDS-uiux — KRDS HTML 컴포넌트 키트 (GitHub)](https://github.com/KRDS-uiux/krds-uiux)
- [KRDS 공식 Figma (@krds)](https://www.figma.com/@krds)

**폰트 (사용자 직접 설치)**
- [Pretendard (GitHub, OFL)](https://github.com/orioncactus/pretendard)
- [pretendard-gov (npm)](https://www.npmjs.com/package/pretendard-gov)

**Claude 공식 스킬**
- [anthropics/skills — canvas-design, brand-guidelines, pptx, docx (GitHub)](https://github.com/anthropics/skills)
- [awesome-claude-skills — 커뮤니티 스킬 모음](https://github.com/travisvn/awesome-claude-skills)

전체 링크 표는 [`resources/RESOURCES.md`](../resources/RESOURCES.md) 참고.
