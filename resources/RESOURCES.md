# 리소스 링크집 (한글 지원 · Claude Design 입력용)

> 폰트와 우수제안서 원본은 사용자가 직접 삽입 예정이므로, 그 외 **Claude에 입력 가능한
> GitHub 저장소 · 코드 · .fig(Figma) 파일**을 큐레이션했습니다.
> 우선순위 순서로 정렬(★ = 강력 추천).

---

## 1. GitHub 저장소 (한글 네이티브 · 무료)

| 저장소 | 용도 | 라이선스 | 링크 |
|---|---|---|---|
| ★ **KRDS-MCP/krds-mcp** | AI(Claude)에 정부 디자인 시스템(색/타이포/간격/37개 컴포넌트)을 **직접 주입하는 MCP 서버**. `npx @krds-mcp/krds-mcp`로 Claude Desktop에 연결하면 Claude가 간격·색을 발명하지 않고 KRDS 값을 인용. | MIT | https://github.com/KRDS-MCP/krds-mcp |
| ★ **KRDS-uiux/krds-uiux** | KRDS **HTML/CSS/SCSS 컴포넌트 키트** + `tokens` 폴더(디자인 토큰). HTML/웹 산출물에 붙여쓰기. `npm install krds-uiux` | KRDS 이용약관 | https://github.com/KRDS-uiux/krds-uiux |
| **orioncactus/pretendard** | 표준 한글 폰트 Pretendard / Pretendard GOV (가변폰트). *폰트는 사용자가 직접 설치* | OFL 1.1 | https://github.com/orioncactus/pretendard |
| **anthropics/skills** | Claude 공식 스킬. `canvas-design`, `brand-guidelines`, `pptx`, `docx` — 디자인 스킬 구조/철학 참고 | Apache 2.0 (문서 스킬은 source-available) | https://github.com/anthropics/skills |
| **travisvn/awesome-claude-skills** | 커뮤니티 Claude 스킬 총망라 (디자인/문서 스킬 발굴용) | — | https://github.com/travisvn/awesome-claude-skills |

**추천 사용법 — 이미 연결해 두었습니다.**
- 이 저장소 루트에 [`​.mcp.json`](../.mcp.json)을 커밋해 두었으므로, **Claude Code에서 이 프로젝트를 열면
  KRDS 서버가 자동 인식**됩니다(최초 1회 서버 신뢰 승인만 하면 됨). 검증: `@krds-mcp/krds-mcp@1.0.7` stdio 정상 기동 확인.
- **Claude Desktop**을 쓰는 경우엔 아래를 `claude_desktop_config.json`에 붙여넣으세요(동일 설정):
  ```json
  {
    "mcpServers": {
      "krds": { "command": "npx", "args": ["-y", "@krds-mcp/krds-mcp"] }
    }
  }
  ```
  설정 파일 위치 — macOS: `~/Library/Application Support/Claude/claude_desktop_config.json`,
  Windows: `%APPDATA%\Claude\claude_desktop_config.json`. 붙여넣은 뒤 Claude Desktop 재시작.
- 전제조건: Node.js 18~21 설치(최초 실행 시 `npx`가 패키지를 내려받음).
- MCP 없이도: `krds-uiux`의 tokens + 이 저장소 `resources/krds-design-tokens.css`를 첨부.

---

## 2. .fig (Figma) 파일 — 복제 후 "채우기"

> **핵심**: Figma community 파일은 "Open in Figma → Duplicate"로 .fig를 자기 계정에 복제할 수 있습니다.
> Claude에는 "새 레이아웃 창작 금지, 이 프레임을 복제 후 텍스트만 교체" 지시와 함께 사용하세요.

| 파일 | 용도 | 한글 | 링크 |
|---|---|---|---|
| ★ **KRDS_v1.0.0 (공식)** | 정부 디자인 시스템 공식 Figma 키트: 색/타이포/변수/컴포넌트/패턴. 제안서 골격을 여기서 복제 | ✅ 네이티브 | https://www.figma.com/community/file/1452915208095182951/krds-v1-0-0 |
| **KRDS 공식 채널 (@krds)** | KRDS가 배포하는 최신 Figma 리소스 모음 | ✅ | https://www.figma.com/@krds |
| **Proposal Templates** | 범용 제안서 템플릿(표지/목차/타임라인/비용). 텍스트만 한글 교체 | 영문(한글 교체 가능) | https://www.figma.com/community/file/1209601248301189157/proposal-templates |
| **Business Proposal Presentation — The Conference Room** | 제안 발표 덱 템플릿 | 영문(한글 교체 가능) | https://www.figma.com/community/file/1250732932146799895/business-proposal-presentation-template-the-conference-room |
| **Project Proposal Template** | 프로젝트 제안서 | 영문(한글 교체 가능) | https://www.figma.com/community/file/1304964781542542409/project-proposal-template |
| **Korean Font Preview (한글 폰트 프리뷰)** | 한글 폰트 조합 미리보기 → 우수제안서에 맞는 폰트 페어링 선택용 | ✅ | https://www.figma.com/community/file/1590247665453113616/korean-font-preview |

**보조 플러그인**
- 한글입숨(Lorem Ipsum 한글판) — 더미 한글 채우기: https://www.figma.com/community/plugin/1218854890608417355

---

## 3. 코드 (이 저장소 내 산출물)

| 파일 | 설명 |
|---|---|
| `resources/krds-design-tokens.css` | KRDS·8pt 그리드 기반 디자인 토큰. Claude에 첨부하거나 HTML에 `<link>` |
| `resources/claude-design-rules.md` | AI 느낌 제거 제약 프롬프트. 시스템/스킬로 주입 |
| `docs/claude-design-anti-ai-guide.md` | 원인 분석 · 해법 · 워크플로우 · 검증 체크리스트 |

---

## 4. 공신력 있는 참고 문서

- KRDS 공식 사이트 — https://www.krds.go.kr/
- KRDS 서체(Typography) 가이드 — https://v04.krds.go.kr/guide/style/style_03.html
- KRDS 리소스 다운로드(Figma/Sketch/XD) — https://www.krds.go.kr/html/site/outline/outline_05.html

## 5. AI 느낌 원인·해법 (실무 블로그)

- llemental — Why AI Presentations Look AI-Generated: https://llemental.com/posts/why-ai-presentations-look-ai-generated
- Presenti.ai — Humanize AI Presentations: https://presenti.ai/blog/humanize-ai-presentations/
- 2Slides — Why AI Slides Look Fake (5 Fixes): https://2slides.com/blog/why-ai-slides-look-fake-and-how-to-fix
- Beautiful.ai — Great Presentations Still Need Design Rules: https://www.beautiful.ai/blog/ai-can-build-slides-fast--but-great-presentations-still-need-design-rules
