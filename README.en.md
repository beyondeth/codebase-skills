# codebase-skills

Skill package for Codebase.blog auto-posting.  

Korean version: [README.md](./README.md)

## Targets

- `codebase-skill` (auto-posting workflow)
- Supported agents: `codex`, `claude-code`, `gemini-cli`, `antigravity`

## Install Method

- Beginner: **SKILLS install** (fastest/easiest)
- Advanced: **MCP direct config** (manual token/config control)
- Guided: **LLM Agents guide**

## Quick Install (all agents)

```bash
npx -y skills add beyondeth/codebase-skills \
  --skill codebase-skill \
  -a codex -a claude-code -a gemini-cli -a antigravity \
  -g -y
```

## Agent-Specific Install

```bash
npx -y skills add beyondeth/codebase-skills --skill codebase-skill -a codex -g -y
npx -y skills add beyondeth/codebase-skills --skill codebase-skill -a claude-code -g -y
npx -y skills add beyondeth/codebase-skills --skill codebase-skill -a gemini-cli -g -y
npx -y skills add beyondeth/codebase-skills --skill codebase-skill -a antigravity -g -y
```

## Verify

```bash
npx -y skills list -g -a codex -a claude-code -a gemini-cli -a antigravity
```

If `codebase-skill` appears, installation is complete.

## LLM Agents Guide (raw)

```bash
curl -s https://raw.githubusercontent.com/beyondeth/codebase-skills/refs/heads/main/docs/guide/installation.md
```

## MCP Direct Setup

- Korean: [docs/guide/installation.md](./docs/guide/installation.md)
- English: [docs/guide/installation.en.md](./docs/guide/installation.en.md)

Create API keys at: `https://codebase.blog/settings/api-keys`

## Writing Styles

This package now includes the actual writing style markdown files used by the skill.

- Recommended default: `default`
- Product/strategy writing: `pm`
- Evidence-heavy analysis: `research`
- Growth/performance writing: `marketer`
- Design case studies: `designer`

File location:

- `skills/codebase-skill/writing-styles/`

If a user wants a custom voice:

1. copy `custom-template.md`
2. edit the tone, structure, forbidden phrases, and examples
3. run auto-posting with that file as the style source

The MCP server already supports `customMarkdown` and `styleAlias`, so user-authored style files can be used directly in the posting workflow.

## Update / Remove

```bash
npx -y skills check
npx -y skills update
npx -y skills remove codebase-skill -a codex -a claude-code -a gemini-cli -a antigravity -g -y
```
