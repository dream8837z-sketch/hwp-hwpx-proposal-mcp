# Claude Design — "AI 느낌" 배제 리서치 & 리소스 모음

한글 제안서를 Claude Design으로 만들 때 **AI가 만든 티**(문단 간격 틀어짐, 템플릿 드리프트, 도형/정렬 오류)를
구조적으로 제거하기 위한 조사 결과와, **Claude Design에 그대로 입력할 수 있는** 자료 모음입니다.

- 바로 붙여넣어 쓰는 디자인 시스템: [`PROPOSAL.DESIGN.md`](./PROPOSAL.DESIGN.md)
- 폰트·우수제안서는 사용자가 직접 삽입 (`{{ }}` 슬롯 참고)

---

## 1. 왜 "AI 티"가 나는가 (원인)

Claude Design은 **맥락(DESIGN.md)이 없으면** 항상 같은 기본 미학으로 수렴합니다:
크림/세리프/테라코타, teal 액센트(`#16d5e6`), 보라→파랑 그라디언트 히어로, 이모지 불릿,
둥근카드+왼쪽 컬러바, 무한 컨테이너 중첩, 전면 가운데 정렬 등. 이것이 이른바 **"AI slop"** 입니다.

문단 간격이 틀어지는 건 **간격 스케일을 강제하지 않아** AI가 문단마다 임의 margin을 넣기 때문이고,
템플릿이 페이지마다 흔들리는 건 **페이지 마스터 재사용 규칙이 없기** 때문이며,
도형 오류는 **radius/정렬 규칙과 출고 전 검수 루프가 없기** 때문입니다.

**해법(공신력 있는 자료들이 공통으로 말하는 공식):**
`DESIGN.md(디자인 시스템 파일)` + `명명된 미학 가족` + `2~3개 브랜드 레퍼런스` +
`8pt 간격 스케일 강제` + `재생성 대신 Tweaks 반복` + `출고 전 자동 검수 체크리스트`.
→ 이 저장소의 [`PROPOSAL.DESIGN.md`](./PROPOSAL.DESIGN.md) 가 이 공식을 한글 제안서용으로 구현한 것입니다.

---

## 2. Claude Design에 입력할 GitHub 링크 (한글 지원 우선)

### 🟢 한글 지원 확인됨
| 리소스 | 설명 | 링크 |
|---|---|---|
| **claude-design-auditor-skill** | 19개 전문 규칙(타이포·간격·WCAG·도형 radius·정렬)로 감사. **한글 완전 지원**(라벨·심각도·리포트 자동 한글화). 도형/간격/문단 오류를 정량 점검. | https://github.com/Ashutos1997/claude-design-auditor-skill |
| **design-with-claude (dwic)** | 41개 무료 디자인 스킬. `npx dwic-audit`로 디자인 시스템 위반을 출고 전 검출. | https://github.com/imsaif/design-with-claude |
| **Toss DESIGN.md** | 한국 핀테크 브랜드. `Toss Product Sans + Noto Sans KR` 기준 — 한글 폰트/톤 레퍼런스로 유용. | https://github.com/rohitg00/awesome-claude-design/blob/main/design-md/playful/toss.md |
| **korean-skill-creator** | 요구사항 기반으로 **한글 Claude 스킬 자동 생성**(SKILL.md + references 구조). | https://lobehub.com/ko/skills/clwmfksek-claude-skills-korean-skill-creator |

### 🔵 핵심 디자인 시스템/스킬 (영문이나 규칙이 언어 무관하게 적용)
| 리소스 | 설명 | 링크 |
|---|---|---|
| **awesome-claude-design** | DESIGN.md 9개 미학 가족, 리믹스 레시피, 안티슬롭 프롬프트팩(`break-default-aesthetic.md`). 가장 방대한 큐레이션. | https://github.com/rohitg00/awesome-claude-design |
| **anthropics/skills — frontend-design** | Anthropic 공식 프론트엔드 디자인 스킬(모델 전반 75% 승률). AI slop 회피 기준. | https://github.com/anthropics/skills/blob/main/skills/frontend-design/SKILL.md |
| **claude-cookbooks — frontend aesthetics** | Anthropic 공식 노트북. 안티슬롭 프롬프팅 가이드. | https://github.com/anthropics/claude-cookbooks/blob/main/coding/prompting_for_frontend_aesthetics.ipynb |
| **jiji262/claude-design-skill** | Claude.ai 내부 Design 시스템 프롬프트를 이식한 포터블 스킬(SKILL.md + references + assets 템플릿). | https://github.com/jiji262/claude-design-skill |
| **google-labs-code/design.md** | DESIGN.md 공식 스펙(Apache 2.0). | https://github.com/google-labs-code/design.md |
| **VoltAgent/awesome-claude-design** | 68개 브랜드 DESIGN.md, 산업별 분류. 레퍼런스 추출용. | https://github.com/VoltAgent/awesome-claude-design |

### DESIGN.md 자동 추출 도구 (우리 브랜드 → DESIGN.md)
- `npx brandmd https://<우리사이트>` → DESIGN.md + CSS 변수 + Tailwind + 다크모드 생성
- **getdesign.md** 웹 뷰어: https://getdesign.md/ (60+ DESIGN.md 브라우징)

---

## 3. .fig 파일 (Figma — 한글 제안서 템플릿)

Figma 커뮤니티 파일을 열고 **Duplicate** 하면 `.fig` 로 내보내거나 그대로 편집할 수 있습니다.
Claude Design에는 스크린샷 또는 Figma URL로 레퍼런스를 넣을 수 있습니다.

| 템플릿 | 설명 | 링크 |
|---|---|---|
| **패스트파이브 제안서 템플릿** | 한국 실무 제안서 레이아웃(한글). 표지·목차·본문 구조 참고. | https://www.figma.com/ko-kr/community/file/1121658805542047854/ |
| **Proposal Templates (Figma 공식)** | 범용 제안서 템플릿 세트. | https://www.figma.com/community/file/1209601248301189157/proposal-templates |
| **Figma 프레젠테이션 무료 템플릿(3,400+)** | 제안서/발표용. "제안서"·"proposal" 검색. | https://www.figma.com/ko-kr/community/presentations |
| **Figma 전략기획 템플릿(60+)** | 사업계획·로드맵 페이지 구성 참고. | https://www.figma.com/templates/strategic-planning/ |
| **공공기관 제안서 레이아웃 아이디어** | 공공 제안서 레이아웃 레퍼런스(핀터레스트 보드). | https://kr.pinterest.com/qkrxodyddl2906/공공기관-제안서-레이아웃/ |

> 팁: Figma 커뮤니티에서 `제안서`, `사업계획서`, `IR deck` 로 검색하면 한글 .fig가 다수 나옵니다.
> 마음에 드는 파일을 Duplicate → 우리 폰트/색으로 교체 후, 그 결과를 Claude Design에 레퍼런스로 투입하세요.

---

## 4. 실행 순서 (Recommended workflow)

1. [`PROPOSAL.DESIGN.md`](./PROPOSAL.DESIGN.md) 의 `{{ }}` 슬롯에 **폰트·브랜드색·우수제안서**를 채운다.
2. Claude Design 새 프로젝트 첫 메시지에 그 파일 전체를 붙여넣는다.
3. "이 DESIGN.md를 엄격히 지켜 표지→목차→본문→도표 페이지 마스터를 먼저 만들라"고 지시.
4. 완성 후 "§7 체크리스트를 스스로 점검하라"고 지시 → 자가 검수.
5. 추가로 **claude-design-auditor-skill**(한글)로 감사해 간격·도형·문단 오류를 정량 확인.
6. 수정은 재생성 대신 **Tweaks**로 반복.

---

## 5. 출처 (Sources)

- [awesome-claude-design (rohitg00)](https://github.com/rohitg00/awesome-claude-design)
- [claude-design-auditor-skill (Ashutos1997)](https://github.com/Ashutos1997/claude-design-auditor-skill)
- [design-with-claude (imsaif)](https://github.com/imsaif/design-with-claude)
- [jiji262/claude-design-skill](https://github.com/jiji262/claude-design-skill)
- [anthropics/skills — frontend-design](https://github.com/anthropics/skills/blob/main/skills/frontend-design/SKILL.md)
- [How to Avoid AI Slop When Using Claude Design (MindStudio)](https://www.mindstudio.ai/blog/claude-design-avoid-ai-slop-design-system)
- [Claude Design 시작하기 (Anthropic 지원센터)](https://support.claude.com/en/articles/14604416-get-started-with-claude-design)
- [Figma 커뮤니티 — 제안서 템플릿](https://www.figma.com/ko-kr/community/file/1121658805542047854/)
