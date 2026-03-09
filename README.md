# codebase-skills

Codebase.blog 자동포스팅을 위한 스킬 패키지입니다.  
설치 목적은 단순합니다. 사용자가 복잡한 MCP 설정을 직접 기억하지 않아도, 에이전트가 Codebase.blog 자동포스팅 워크플로를 올바르게 따라가게 만드는 것입니다.

English version: [README.en.md](./README.en.md)

## 이 패키지가 하는 일

- `codebase-skill` 자동포스팅 워크플로를 설치합니다.
- 에이전트가 `skill route (mcporter + OAuth)`와 `mcp route (direct MCP)`를 구분하도록 안내합니다.
- 글쓰기 스타일 가이드와 실제 스타일 markdown 파일을 함께 제공합니다.
- 사용자가 만든 커스텀 스타일 파일도 자동포스팅 흐름에 연결할 수 있게 합니다.

지원 에이전트:

- `codex`
- `claude-code`
- `gemini-cli`
- `antigravity`

## 먼저 무엇을 선택해야 하나요?

설치 방식은 2가지입니다.

- `SKILLS 설치`  
  가장 쉬운 방법입니다. 추천 경로입니다. 에이전트에 자동포스팅 사용법과 스타일 가이드를 설치합니다.
- `MCP 직접 설정`  
  API 키, MCP 설정, 토큰 정책을 직접 제어하고 싶은 고급 사용자용입니다.

간단히 말하면:

- 대부분의 사용자는 `SKILLS 설치`
- 직접 MCP 설정을 관리하고 싶으면 `MCP 직접 설정`

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

중요한 점:

- `SKILLS 설치`는 스킬 문서와 스타일 파일을 에이전트에 넣는 단계입니다.
- API 키를 직접 저장하는 방식이 아니라, 에이전트가 skill 문서에 따라 OAuth 또는 MCP direct 흐름을 안내하도록 만드는 방식입니다.

## MCP 직접 설정

직접 MCP를 붙이고 싶다면 아래 문서를 보세요.

- 한국어 설치 가이드: [docs/guide/installation.md](./docs/guide/installation.md)
- English install guide: [docs/guide/installation.en.md](./docs/guide/installation.en.md)

API 키는 `https://codebase.blog/settings/api-keys`에서 생성합니다.

## 첫 사용 흐름

사용자가 실제로 자동포스팅을 시작하면 흐름은 보통 이렇습니다.

1. 에이전트가 설치된 skill 또는 MCP 경로를 선택합니다.
2. OAuth 또는 API 키 인증 상태를 확인합니다.
3. 글쓰기 스타일을 선택합니다.
4. 스타일 가이드를 기준으로 글을 작성합니다.
5. 최종적으로 `create_post`로 발행합니다.

즉, 이 패키지는 단순한 설치 파일 모음이 아니라,  
`인증 → 스타일 선택 → 작성 → 발행` 흐름을 일관되게 유지하기 위한 패키지입니다.

## 글쓰기 스타일이 왜 중요한가요?

글쓰기 스타일은 “어떤 말투로 쓸지” 정도가 아니라, 아래를 함께 결정합니다.

- 글의 구조
- 문장 톤
- 강조 방식
- 어떤 종류의 근거를 넣을지
- 어떤 독자를 상정할지

예를 들어:

- `default`는 가장 무난한 기술 블로그 기본형
- `pm`은 제품 의사결정과 전략 설명에 적합
- `research`는 근거, 실험, 한계를 엄격히 다루는 글에 적합
- `marketer`는 성장 실험, 전환, 카피 테스트 결과 정리에 적합
- `designer`는 UX 맥락과 디자인 판단을 설명하는 케이스 스터디에 적합

스타일 상세 설명은 여기서 볼 수 있습니다.

- 스타일 상세 문서(한국어): [docs/guide/writing-styles.md](./docs/guide/writing-styles.md)
- Style guide details (English): [docs/guide/writing-styles.en.md](./docs/guide/writing-styles.en.md)
- 실제 스타일 파일: [skills/codebase-skill/writing-styles](./skills/codebase-skill/writing-styles)

스타일을 잘 모르겠다면 `default`부터 시작하면 됩니다.

## 실제 스타일 파일이 포함되어 있습니다

이 패키지에는 설명만 있는 것이 아니라, 에이전트가 참고할 수 있는 실제 markdown 스타일 파일이 포함되어 있습니다.

포함 파일:

- `_common.md`
- `default.md`
- `novel.md`
- `podcast.md`
- `vibe.md`
- `research.md`
- `pm.md`
- `designer.md`
- `marketer.md`

즉, 사용자는 “스타일 이름만 선택”하는 것이 아니라,  
실제로 어떤 규칙이 들어 있는지 파일을 열어서 확인할 수 있습니다.

## 커스텀 스타일도 사용할 수 있습니다

사용자가 자기만의 문체, 금지 표현, 구조 규칙을 가지고 있다면 기본 스타일 대신 커스텀 스타일 파일을 쓸 수 있습니다.

시작 파일:

- [custom-template.md](./skills/codebase-skill/writing-styles/custom-template.md)

권장 흐름:

1. `custom-template.md`를 복사합니다.
2. 원하는 톤, 구조, 금지 표현, 예시 문단을 채웁니다.
3. 에이전트가 그 파일을 읽습니다.
4. 에이전트가 그 내용을 `customMarkdown`으로 MCP에 전달합니다.
5. 그 가이드를 기준으로 글을 작성하고 발행합니다.

현재 MCP 서버는 `customMarkdown`과 `styleAlias`를 지원하므로,  
사용자 커스텀 스타일 파일을 실제 자동포스팅의 source of truth로 사용할 수 있습니다.

## LLM Agents용 설치 가이드

아래 raw 문서를 에이전트에게 그대로 전달하면,  
`SKILLS 설치 vs MCP 직접 설정` 선택부터 단계적으로 안내할 수 있습니다.

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

- `-g` 옵션은 전역 설치입니다.
- `-g`를 빼면 현재 프로젝트에만 설치됩니다.

## 문서 바로가기

- 설치 가이드(한국어): [docs/guide/installation.md](./docs/guide/installation.md)
- Installation guide (English): [docs/guide/installation.en.md](./docs/guide/installation.en.md)
- 스타일 가이드(한국어): [docs/guide/writing-styles.md](./docs/guide/writing-styles.md)
- Style guide (English): [docs/guide/writing-styles.en.md](./docs/guide/writing-styles.en.md)
- skill 메인 문서: [skills/codebase-skill/SKILL.md](./skills/codebase-skill/SKILL.md)
- MCPorter 치트시트: [skills/codebase-skill/MCPORTER_SKILL.md](./skills/codebase-skill/MCPORTER_SKILL.md)

## 레이아웃

```text
skills/
  codebase-skill/
    SKILL.md
    HEARTBEAT.md
    MCPORTER_SKILL.md
    MESSAGING.md
    writing-styles/
      README.md
      _common.md
      default.md
      novel.md
      podcast.md
      vibe.md
      research.md
      pm.md
      designer.md
      marketer.md
      custom-template.md

docs/
  guide/
    installation.md
    installation.en.md
    writing-styles.md
    writing-styles.en.md
```
