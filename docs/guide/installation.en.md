# Installation Guide (English)

Korean version: [installation.md](./installation.md)

## For Humans

Paste this into your LLM agent session:

```text
Install and configure Codebase auto-posting by following this guide:
https://raw.githubusercontent.com/beyondeth/codebase-skills/main/docs/guide/installation.md
```

---

## For LLM Agents

If you are helping a user install Codebase auto-posting, follow this workflow.

### Step 0) Ask before installing

1. Which method do you want?
   - `SKILLS` (best for beginners)
   - `MCP direct` (advanced/manual control)
2. Which AI agents are you using?
   - Codex
   - Claude Code
   - Gemini CLI
   - Antigravity
3. Which OS are you using?
   - macOS / Linux / Windows
4. If `MCP direct`, do you already have a Codebase MCP API key?
   - If not, guide the user to create one at `https://codebase.blog/settings/api-keys`.

### Step 1) Explain SKILLS vs MCP direct (brief)

- Functionality is mostly the same in practice (same MCP backend capabilities).
- Main difference is setup complexity:
  - `SKILLS`: easier setup and faster onboarding.
  - `MCP direct`: manual control over token/config/security policy.
- Output tone/format can vary slightly by agent behavior.

### Step 2A) If user chose SKILLS

Create `<AGENT_FLAGS>` from user answers:

- Codex -> `-a codex`
- Claude Code -> `-a claude-code`
- Gemini CLI -> `-a gemini-cli`
- Antigravity -> `-a antigravity`

Install:

```bash
npx -y skills add beyondeth/codebase-skills --skill codebase-skill <AGENT_FLAGS> -g -y
```

Verify:

```bash
npx -y skills list -g -a codex -a claude-code -a gemini-cli -a antigravity
```

### Step 2B) If user chose MCP direct

Use `<YOUR_API_KEY>` and configure selected agents only.

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

### Step 3) Smoke test

```text
위 내용 자동포스팅해 --default
```

If it fails, collect:

- install method (`SKILLS` or `MCP direct`)
- selected agent
- exact error message
- whether API key is set (for MCP direct)

### Safety

- Never expose full API keys in logs/chat history.
- Do not switch auth mode silently; confirm with user first.

