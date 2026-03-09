# MCP direct 설치 가이드

이 문서는 `MCP direct`만 설명합니다.

초보자라면 먼저:

- [SKILLS 설치 가이드](./skills-installation.md)

## 누구에게 맞나요?

- MCP 설정을 직접 관리하고 싶은 사용자
- API 키와 설정 파일을 직접 다루고 싶은 사용자
- Codex / Claude / Gemini / Antigravity에 MCP를 수동으로 붙이고 싶은 사용자

## 준비물

1. Codebase MCP API 키
2. 사용 에이전트 이름
3. 운영체제

API 키 생성:

- `https://codebase.blog/settings/api-keys`

## 에이전트별 예시

### Codex

```bash
export CODEBASE_MCP_TOKEN="<YOUR_API_KEY>"
codex mcp add codebase-blog-mcp --url https://mcp.codebase.blog/mcp --bearer-token-env-var CODEBASE_MCP_TOKEN
codex mcp get codebase-blog-mcp
```

```powershell
$Env:CODEBASE_MCP_TOKEN = "<YOUR_API_KEY>"
codex mcp add codebase-blog-mcp --url https://mcp.codebase.blog/mcp --bearer-token-env-var CODEBASE_MCP_TOKEN
codex mcp get codebase-blog-mcp
```

### Claude Code

```bash
claude mcp add --transport http codebase-blog-mcp https://mcp.codebase.blog/mcp --header "Authorization: Bearer <YOUR_API_KEY>"
```

### Gemini CLI

```json
{
  "mcpServers": {
    "codebase-blog-mcp": {
      "httpUrl": "https://mcp.codebase.blog/mcp",
      "headers": {
        "Authorization": "Bearer <YOUR_API_KEY>",
        "Accept": "application/json, text/event-stream"
      }
    }
  }
}
```

### Antigravity

```json
{
  "mcpServers": {
    "codebase-blog-mcp": {
      "serverUrl": "https://mcp.codebase.blog/mcp",
      "headers": {
        "Authorization": "Bearer <YOUR_API_KEY>",
        "Accept": "application/json, text/event-stream"
      }
    }
  }
}
```

## 주의

- 초보자는 `SKILLS 설치`가 더 적합합니다.
- 처음에는 `SKILLS 설치`와 `MCP direct`를 동시에 섞지 마세요.
- API 키 전체값을 채팅이나 스크린샷에 노출하지 마세요.
