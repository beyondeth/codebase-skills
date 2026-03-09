# codebase-skills

Codebase.blog 자동포스팅을 위한 스킬 패키지입니다.  

English version: [README.en.md](./README.en.md)

## 지원 대상

- `codebase-skill` (자동포스팅 워크플로)
- 지원 에이전트: `codex`, `claude-code`, `gemini-cli`, `antigravity`

## 설치 방법 선택

- 초보자: **SKILLS 설치** (가장 간단)
- 고급 사용자: **MCP 직접 설정** (토큰/설정 직접 제어)
- 자동 안내: **LLM Agents 가이드** 사용

## 빠른 설치 (전체 에이전트)

```bash
npx -y skills add beyondeth/codebase-skills \
  --skill codebase-skill \
  -a codex -a claude-code -a gemini-cli -a antigravity \
  -g -y
```

## 에이전트별 설치

```bash
npx -y skills add beyondeth/codebase-skills --skill codebase-skill -a codex -g -y
npx -y skills add beyondeth/codebase-skills --skill codebase-skill -a claude-code -g -y
npx -y skills add beyondeth/codebase-skills --skill codebase-skill -a gemini-cli -g -y
npx -y skills add beyondeth/codebase-skills --skill codebase-skill -a antigravity -g -y
```

## 설치 확인

```bash
npx -y skills list -g -a codex -a claude-code -a gemini-cli -a antigravity
```

`codebase-skill`이 표시되면 정상입니다.

## LLM Agents용 설치 가이드

아래 raw 문서를 에이전트에게 전달하면,  
`SKILLS vs MCP` 선택 질문부터 설치까지 단계적으로 안내할 수 있습니다.

```bash
curl -s https://raw.githubusercontent.com/beyondeth/codebase-skills/refs/heads/main/docs/guide/installation.md
```

## MCP 직접 설정

MCP 직접 설정은 아래 문서 참고:

- 기본(한국어): [docs/guide/installation.md](./docs/guide/installation.md)
- English: [docs/guide/installation.en.md](./docs/guide/installation.en.md)

API 키 생성은 `https://codebase.blog/settings/api-keys`에서 진행합니다.

## 글쓰기 스타일

이 스킬에는 실제 글쓰기 스타일 파일이 함께 들어 있습니다.

- 기본 추천: `default`
- 제품/전략 글: `pm`
- 근거 중심 분석: `research`
- 성장/마케팅 글: `marketer`
- 디자인 케이스 스터디: `designer`

실제 파일 위치:

- `skills/codebase-skill/writing-styles/`

사용자가 자기만의 문체를 쓰고 싶다면:

1. `custom-template.md`를 복사
2. 원하는 톤과 금지 표현을 수정
3. 그 파일을 기반으로 자동포스팅 실행

현재 MCP 서버는 `customMarkdown` + `styleAlias`를 지원하므로, 사용자 커스텀 스타일 파일도 그대로 발행 흐름에 태울 수 있습니다.

## 업데이트 / 제거

```bash
npx -y skills check
npx -y skills update
npx -y skills remove codebase-skill -a codex -a claude-code -a gemini-cli -a antigravity -g -y
```

## 참고

- `-g` 옵션: 전역 설치(모든 프로젝트에서 사용)
- `-g` 제거 시: 현재 프로젝트에만 설치

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
```
