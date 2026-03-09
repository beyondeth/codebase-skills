# SKILLS 설치 가이드

이 문서는 `SKILLS 설치`만 설명합니다.

MCP를 직접 붙이고 싶다면:

- [MCP direct 설치 가이드](./mcp-direct.md)

## 누구에게 맞나요?

- 초보자
- 빠르게 자동포스팅을 시작하고 싶은 사용자
- MCP 설정 파일을 직접 관리하고 싶지 않은 사용자

## 설치

```bash
npx -y skills add beyondeth/codebase-skills \
  --skill codebase-skill \
  -a codex -a claude-code -a gemini-cli -a antigravity \
  -g -y
```

에이전트별 설치:

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

`codebase-skill`이 보이면 완료입니다.

## 설치 후 무엇이 들어가나요?

- 자동포스팅 workflow 문서
- MCPorter + OAuth 사용 가이드
- 실제 글쓰기 스타일 파일
- 커스텀 스타일 템플릿

다음 읽을 문서:

- [글쓰기 스타일 가이드](./writing-styles.md)
- [skill 메인 문서](../../skills/codebase-skill/SKILL.md)
