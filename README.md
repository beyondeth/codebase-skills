# codebase-skills

Codebase.blog 자동포스팅을 에이전트에 붙이기 위한 스킬 패키지입니다.  
목표는 단순합니다. 설치 경로를 헷갈리지 않게 만들고, `인증 -> 스타일 선택 -> 작성 -> 발행` 흐름을 일관되게 유지하는 것입니다.

English version: [README.en.md](./README.en.md)

## 누구를 위한 패키지인가요?

- Codebase.blog에 자동포스팅을 붙이고 싶은 사용자
- MCP 설정을 처음 접하는 사용자
- 글쓰기 스타일 가이드와 실제 스타일 파일을 같이 보고 싶은 사용자
- 커스텀 스타일 파일을 기반으로 자동포스팅하고 싶은 사용자

지원 에이전트:

- `codex`
- `claude-code`
- `gemini-cli`
- `antigravity`

## 먼저 설치 경로를 하나만 고르세요

`SKILLS 설치`와 `MCP direct`는 목적이 다릅니다. 둘을 섞어서 시작하지 마세요.

| 경로 | 누구에게 적합한가 | 특징 |
| --- | --- | --- |
| `SKILLS 설치` | 대부분의 사용자 | 가장 쉬움. 스킬 문서, 스타일 가이드, 설치 흐름까지 같이 들어감 |
| `MCP direct` | 고급 사용자 | API 키, MCP 설정, 보안 정책을 직접 관리 |

- 초보자라면 `SKILLS 설치`
- MCP 설정 파일을 직접 다루고 싶다면 `MCP direct`

## 빠른 시작: SKILLS 설치

가장 추천하는 시작 방법입니다.

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

## 설치 후 실제로 무엇이 들어가나요?

- 자동포스팅 workflow 문서
- MCPorter + OAuth 사용 가이드
- 실제 글쓰기 스타일 markdown 파일
- 커스텀 스타일 템플릿

즉, 이 패키지는 단순히 명령어 한 줄만 제공하는 것이 아니라,  
에이전트가 Codebase.blog 자동포스팅을 안정적으로 수행하도록 문서와 스타일 소스를 함께 설치합니다.

## 설치 문서

- 설치 경로 선택: [docs/guide/installation.md](./docs/guide/installation.md)
- `SKILLS 설치` 가이드: [docs/guide/skills-installation.md](./docs/guide/skills-installation.md)
- `MCP direct` 가이드: [docs/guide/mcp-direct.md](./docs/guide/mcp-direct.md)

API 키 생성:

- `https://codebase.blog/settings/api-keys`

## 글쓰기 스타일이 왜 중요한가요?

글쓰기 스타일은 단순히 말투만 정하는 것이 아닙니다. 아래를 함께 결정합니다.

- 글의 구조
- 문장 톤
- 어떤 근거를 넣을지
- 어떤 독자를 상정할지
- 최종 글이 얼마나 분석형인지, 제품형인지, 설명형인지

스타일을 잘 모르면 `default`부터 시작하면 됩니다.

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

## 실제 스타일 파일이 같이 들어 있습니다

이 패키지에는 설명만 있는 것이 아니라, 실제 markdown 스타일 파일이 포함되어 있습니다.

- `_common.md`
- `default.md`
- `novel.md`
- `podcast.md`
- `vibe.md`
- `research.md`
- `pm.md`
- `designer.md`
- `marketer.md`

즉, 사용자는 스타일 이름만 고르는 것이 아니라  
실제 규칙 파일을 열어서 문체와 구조를 직접 확인할 수 있습니다.

## 커스텀 스타일도 사용할 수 있습니다

브랜드 문체, 금지 표현, 문단 구조, 제목 규칙이 이미 정해져 있다면 기본 스타일보다 커스텀 스타일이 더 적합합니다.

시작 파일:

- [custom-template.md](./skills/codebase-skill/writing-styles/custom-template.md)

권장 흐름:

1. `custom-template.md`를 복사합니다.
2. 원하는 톤, 구조, 금지 표현, 예시 문단을 작성합니다.
3. 에이전트가 그 파일을 읽습니다.
4. 에이전트가 그 내용을 `customMarkdown`으로 MCP에 전달합니다.
5. 그 가이드를 기준으로 글을 작성하고 발행합니다.

현재 MCP 서버는 `customMarkdown`과 `styleAlias`를 지원하므로,  
사용자가 만든 스타일 파일을 실제 자동포스팅의 기준 파일로 사용할 수 있습니다.

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
