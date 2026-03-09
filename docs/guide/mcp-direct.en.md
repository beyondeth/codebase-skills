# MCP Direct Installation Guide

This document covers `MCP direct` only.

If you are a beginner, start here instead:

- [SKILLS installation guide](./skills-installation.en.md)

## Who is this for?

- users who want to manage MCP config directly
- users who want direct control over API keys and config files
- users who want to connect MCP manually in Codex / Claude / Gemini / Antigravity

## Requirements

1. a Codebase MCP API key
2. your agent name
3. your operating system

Create the API key here:

- `https://codebase.blog/settings/api-keys`

## Per-agent examples

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

## Important notes

- Beginners should usually use `SKILLS install` instead.
- Do not mix `SKILLS install` and `MCP direct` during initial setup.
- Never expose the full API key in chat or screenshots.
