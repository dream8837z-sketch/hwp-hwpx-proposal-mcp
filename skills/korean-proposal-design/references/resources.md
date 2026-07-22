# 리소스 — 한글 지원 GitHub 스킬 · DESIGN.md · Figma(.fig)

Claude Design에 함께 투입하거나 감사 도구로 병행 사용할 수 있는 외부 자료 모음.
(디자인 규칙 자체는 중복을 피해 `assets/PROPOSAL.DESIGN.md` 에만 정의되어 있음.)

## 🟢 한글 지원 확인됨
| 리소스 | 설명 | 링크 |
|---|---|---|
| claude-design-auditor-skill | 19개 전문 규칙(타이포·간격·radius·정렬) 감사. **한글 완전 지원**(라벨·심각도·리포트 자동 한글화). 출력물의 간격·도형·문단 오류 정량 점검용. | https://github.com/Ashutos1997/claude-design-auditor-skill |
| design-with-claude (dwic) | 41개 무료 디자인 스킬. `npx dwic-audit`로 출고 전 디자인 시스템 위반 검출. | https://github.com/imsaif/design-with-claude |
| Toss DESIGN.md | 한국 핀테크 브랜드(`Toss Product Sans + Noto Sans KR`). 한글 폰트/톤 레퍼런스. | https://github.com/rohitg00/awesome-claude-design/blob/main/design-md/playful/toss.md |
| korean-skill-creator | 요구사항 기반 **한글 Claude 스킬 자동 생성**(SKILL.md + references 구조). | https://lobehub.com/ko/skills/clwmfksek-claude-skills-korean-skill-creator |

## 🔵 핵심 디자인 시스템/스킬 (규칙은 언어 무관 적용)
| 리소스 | 설명 | 링크 |
|---|---|---|
| awesome-claude-design | DESIGN.md 9개 미학 가족 + 안티슬롭 프롬프트팩(`break-default-aesthetic.md`). | https://github.com/rohitg00/awesome-claude-design |
| anthropics/skills — frontend-design | Anthropic 공식 프론트엔드 디자인 스킬(모델 전반 75% 승률). | https://github.com/anthropics/skills/blob/main/skills/frontend-design/SKILL.md |
| claude-cookbooks — frontend aesthetics | Anthropic 공식 안티슬롭 프롬프팅 노트북. | https://github.com/anthropics/claude-cookbooks/blob/main/coding/prompting_for_frontend_aesthetics.ipynb |
| jiji262/claude-design-skill | Claude.ai 내부 Design 프롬프트 이식 포터블 스킬(SKILL.md+references+assets). | https://github.com/jiji262/claude-design-skill |
| google-labs-code/design.md | DESIGN.md 공식 스펙(Apache 2.0). | https://github.com/google-labs-code/design.md |
| VoltAgent/awesome-claude-design | 68개 브랜드 DESIGN.md, 산업별 분류. | https://github.com/VoltAgent/awesome-claude-design |

### DESIGN.md 자동 추출 도구
- `npx brandmd https://<우리사이트>` → DESIGN.md + CSS 변수 + Tailwind + 다크모드 생성
- getdesign.md 웹 뷰어: https://getdesign.md/ (60+ DESIGN.md 브라우징)

## .fig (Figma — 한글 제안서 템플릿)
Figma 커뮤니티 파일을 **Duplicate** 후 `.fig` 내보내기/편집. Claude Design엔 스크린샷/URL로 투입.

| 템플릿 | 설명 | 링크 |
|---|---|---|
| 패스트파이브 제안서 템플릿 | 한국 실무 제안서(한글). 표지·목차·본문 구조. | https://www.figma.com/ko-kr/community/file/1121658805542047854/ |
| Proposal Templates (Figma 공식) | 범용 제안서 세트. | https://www.figma.com/community/file/1209601248301189157/proposal-templates |
| Figma 프레젠테이션 무료 템플릿(3,400+) | "제안서"·"proposal" 검색. | https://www.figma.com/ko-kr/community/presentations |
| Figma 전략기획 템플릿(60+) | 사업계획·로드맵 구성. | https://www.figma.com/templates/strategic-planning/ |
| 공공기관 제안서 레이아웃 아이디어 | 공공 제안서 레퍼런스 보드. | https://kr.pinterest.com/qkrxodyddl2906/공공기관-제안서-레이아웃/ |

> 팁: Figma 커뮤니티에서 `제안서`, `사업계획서`, `IR deck` 검색 → Duplicate → 우리 폰트/색 교체 → 결과를 Claude Design 레퍼런스로 투입.

## 출처 (Sources)
- awesome-claude-design (rohitg00) — https://github.com/rohitg00/awesome-claude-design
- claude-design-auditor-skill (Ashutos1997) — https://github.com/Ashutos1997/claude-design-auditor-skill
- design-with-claude (imsaif) — https://github.com/imsaif/design-with-claude
- jiji262/claude-design-skill — https://github.com/jiji262/claude-design-skill
- anthropics/skills — frontend-design — https://github.com/anthropics/skills/blob/main/skills/frontend-design/SKILL.md
- MindStudio: Avoid AI Slop — https://www.mindstudio.ai/blog/claude-design-avoid-ai-slop-design-system
- Claude Design 시작하기(Anthropic) — https://support.claude.com/en/articles/14604416-get-started-with-claude-design
- Figma 제안서 템플릿 — https://www.figma.com/ko-kr/community/file/1121658805542047854/
