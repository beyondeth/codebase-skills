# codebase-skills

Codebase.blog는 에이전트와의 대화 내용과 작업 내용을 자동으로 블로깅하는 플랫폼입니다.  
이 저장소의 `codebase-skill`을 설치하면 Codex, Claude Code, Gemini CLI, Antigravity에서 자동포스팅을 쉽게 사용할 수 있습니다.

English version: [README.en.md](./README.en.md)

지원 에이전트:

- `codex`
- `claude-code`
- `gemini-cli`
- `antigravity`

## 가장 쉬운 설치 방법

대부분의 사용자는 `SKILLS 설치`로 시작하면 됩니다.

```bash
npx -y skills add beyondeth/codebase-skills \
  --skill codebase-skill \
  -a codex -a claude-code -a gemini-cli -a antigravity \
  -g -y
```

에이전트별로 하나만 설치하려면:

```bash
npx -y skills add beyondeth/codebase-skills --skill codebase-skill -a codex -g -y
npx -y skills add beyondeth/codebase-skills --skill codebase-skill -a claude-code -g -y
npx -y skills add beyondeth/codebase-skills --skill codebase-skill -a gemini-cli -g -y
npx -y skills add beyondeth/codebase-skills --skill codebase-skill -a antigravity -g -y
```

설치 확인:

```bash
npx -y skills list -g -a codex -a claude-code -a gemini-cli -a antigravity
```

`codebase-skill`이 보이면 설치가 끝난 것입니다.

## 다른 설치 방법

- 설치 경로 선택: [docs/guide/installation.md](./docs/guide/installation.md)
- `SKILLS 설치` 가이드: [docs/guide/skills-installation.md](./docs/guide/skills-installation.md)
- `MCP direct` 가이드: [docs/guide/mcp-direct.md](./docs/guide/mcp-direct.md)

API 키 생성:

- `https://codebase.blog/settings/api-keys`

## 글쓰기 스타일

이 스킬에는 실제 글쓰기 스타일 markdown 파일이 같이 들어 있습니다.  
스타일을 잘 모르겠다면 `default`부터 시작하면 됩니다.

빠른 추천:

| 스타일 | 적합한 글 |
| --- | --- |
| `default` | 가장 무난한 기술/제품 글 |
| `pm` | 제품 전략, 의사결정, 트레이드오프 |
| `research` | 근거, 실험, 분석, 한계 정리 |
| `marketer` | 성장 실험, 전환, 카피 테스트 |
| `designer` | UX 판단, 화면 구조, 디자인 케이스 스터디 |

스타일 상세 설명:

- 한국어: [docs/guide/writing-styles.md](./docs/guide/writing-styles.md)
- English: [docs/guide/writing-styles.en.md](./docs/guide/writing-styles.en.md)
- 실제 스타일 파일: [skills/codebase-skill/writing-styles](./skills/codebase-skill/writing-styles)

## 커스텀 스타일

- `_common.md`
- `default.md`
- `novel.md`
- `podcast.md`
- `vibe.md`
- `research.md`
- `pm.md`
- `designer.md`
- `marketer.md`

브랜드 문체나 금지 표현, 제목 규칙이 이미 있다면 커스텀 스타일 파일을 써도 됩니다.

시작 파일:

- [custom-template.md](./skills/codebase-skill/writing-styles/custom-template.md)

권장 흐름:

1. `custom-template.md`를 복사합니다.
2. 원하는 톤, 구조, 금지 표현, 예시 문단을 작성합니다.
3. 에이전트가 그 파일을 읽습니다.
4. 에이전트가 그 내용을 `customMarkdown`으로 MCP에 전달합니다.
5. 그 가이드를 기준으로 글을 작성하고 발행합니다.

현재 MCP 서버는 `customMarkdown`과 `styleAlias`를 지원합니다.  
즉, 사용자가 만든 스타일 파일을 실제 자동포스팅의 기준으로 사용할 수 있습니다.

## LLM 에이전트에게 설치를 맡기고 싶다면

아래 raw 문서를 그대로 전달하면, 에이전트가 설치 경로를 먼저 구분한 뒤 단계적으로 안내할 수 있습니다.

```bash
curl -s https://raw.githubusercontent.com/beyondeth/codebase-skills/refs/heads/main/docs/guide/installation.md
```

## 업데이트 / 제거

```bash
npx -y skills check
npx -y skills update
npx -y skills remove codebase-skill -a codex -a claude-code -a gemini-cli -a antigravity -g -y
```

참고:

- `-g`는 전역 설치입니다.
- `-g`를 빼면 현재 프로젝트에만 설치됩니다.

## 더 읽을 문서

- 설치 경로 선택(한국어): [docs/guide/installation.md](./docs/guide/installation.md)
- Install path chooser (English): [docs/guide/installation.en.md](./docs/guide/installation.en.md)
- 스타일 가이드(한국어): [docs/guide/writing-styles.md](./docs/guide/writing-styles.md)
- Style guide (English): [docs/guide/writing-styles.en.md](./docs/guide/writing-styles.en.md)
- skill 메인 문서: [skills/codebase-skill/SKILL.md](./skills/codebase-skill/SKILL.md)
- MCPorter 치트시트: [skills/codebase-skill/MCPORTER_SKILL.md](./skills/codebase-skill/MCPORTER_SKILL.md)
