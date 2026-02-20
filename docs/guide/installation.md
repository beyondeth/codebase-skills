# 설치 가이드 (Korean)

English version: [installation.en.md](./installation.en.md)

## For Humans

아래 문장을 LLM 에이전트 채팅에 그대로 붙여 넣으세요:

```text
Codebase 자동포스팅 설치를 이 가이드대로 진행해줘:
https://raw.githubusercontent.com/beyondeth/codebase-skills/refs/heads/main/docs/guide/installation.md
```

---

## For LLM Agents

Codebase 자동포스팅 설치를 도와주는 에이전트라면 아래 순서를 따르세요.

### Step 0) 설치 전에 먼저 질문

1. 어떤 방식으로 설치할까요?
   - `SKILLS` (초보자/빠른 시작)
   - `MCP direct` (고급 사용자/수동 제어)
2. 어떤 AI 에이전트를 사용하나요?
   - Codex
   - Claude Code
   - Gemini CLI
   - Antigravity
3. OS는 무엇인가요?
   - macOS / Linux / Windows
4. (`MCP direct` 선택 시) Codebase MCP API 키를 이미 가지고 있나요?
   - 없다면 `https://codebase.blog/settings/api-keys`에서 생성하도록 안내

### Step 1) SKILLS vs MCP 차이 설명 (짧게)

- 기능은 대부분 동일함 (같은 MCP 백엔드 기능 사용)
- 차이는 설정 난이도
  - `SKILLS`: 설치와 사용이 단순
  - `MCP direct`: 토큰/설정/보안 정책을 직접 제어
- 에이전트별 동작 차이로 출력 톤/형식은 약간 달라질 수 있음

### Step 2A) 사용자가 SKILLS를 선택한 경우

사용자 답변으로 `<AGENT_FLAGS>` 조합:

- Codex -> `-a codex`
- Claude Code -> `-a claude-code`
- Gemini CLI -> `-a gemini-cli`
- Antigravity -> `-a antigravity`

설치:

```bash
npx -y skills add beyondeth/codebase-skills --skill codebase-skill <AGENT_FLAGS> -g -y
```

검증:

```bash
npx -y skills list -g -a codex -a claude-code -a gemini-cli -a antigravity
```

### Step 2B) 사용자가 MCP direct를 선택한 경우

`<YOUR_API_KEY>`를 실제 키로 바꿔 선택한 에이전트만 설정합니다.

#### Codex (CLI)

```bash
# macOS / Linux
export CODEBASE_MCP_TOKEN="<YOUR_API_KEY>"
codex mcp add codebase-blog-mcp --url https://mcp.codebase.blog/mcp --bearer-token-env-var CODEBASE_MCP_TOKEN
codex mcp get codebase-blog-mcp
```

```powershell
# Windows PowerShell
$Env:CODEBASE_MCP_TOKEN = "<YOUR_API_KEY>"
codex mcp add codebase-blog-mcp --url https://mcp.codebase.blog/mcp --bearer-token-env-var CODEBASE_MCP_TOKEN
codex mcp get codebase-blog-mcp
```

#### Claude Code

```bash
claude mcp add --transport http codebase-blog-mcp https://mcp.codebase.blog/mcp --header "Authorization: Bearer <YOUR_API_KEY>"
```

#### Gemini CLI (`~/.gemini/settings.json`)

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

#### Antigravity (`mcp_config.json`)

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

### Step 3) 스모크 테스트

```text
위 내용 자동포스팅해 --default
```

실패 시 아래를 함께 수집:

- 설치 방식 (`SKILLS` / `MCP direct`)
- 사용 에이전트
- 에러 원문
- (`MCP direct`) API 키 설정 여부

### 안전 수칙

- API 키 전체값을 채팅/로그에 노출하지 말 것
- 인증 모드(OAuth/API Key)를 임의로 변경하지 말고 사용자에게 먼저 확인할 것

