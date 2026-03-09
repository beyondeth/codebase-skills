# SKILLS Installation Guide

This document covers `SKILLS install` only.

If you want to connect MCP directly instead:

- [MCP direct installation guide](./mcp-direct.en.md)

## Who is this for?

- beginners
- users who want the fastest auto-posting setup
- users who do not want to manage MCP config files directly

## Install

```bash
npx -y skills add beyondeth/codebase-skills \
  --skill codebase-skill \
  -a codex -a claude-code -a gemini-cli -a antigravity \
  -g -y
```

Single-agent install:

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

If `codebase-skill` appears, setup is complete.

## What gets installed?

- the auto-posting workflow docs
- MCPorter + OAuth usage guidance
- the actual writing style files
- the custom style template

Recommended next reading:

- [Writing styles guide](./writing-styles.en.md)
- [Main skill doc](../../skills/codebase-skill/SKILL.md)
