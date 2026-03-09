# codebase-skills

Skill package for Codebase.blog auto-posting.  
The purpose of this package is simple: let AI agents follow the Codebase.blog posting workflow correctly without forcing end users to memorize raw MCP setup details.

Korean version: [README.md](./README.md)

## What this package does

- installs the `codebase-skill` auto-posting workflow
- helps agents distinguish between `skill route (mcporter + OAuth)` and `mcp route (direct MCP)`
- bundles writing style guides and the actual markdown style files
- supports user-authored custom style files as part of the posting workflow

Supported agents:

- `codex`
- `claude-code`
- `gemini-cli`
- `antigravity`

## Which install path should you choose?

There are two ways to use Codebase auto-posting.

- `SKILLS install`  
  Best for most users. Recommended default. Installs the workflow instructions and style guides for your agent.
- `MCP direct`  
  Best for advanced users who want direct control over API keys, MCP config, and security policy.

In short:

- most users should start with `SKILLS install`
- use `MCP direct` only if you want to manage the MCP connection yourself

## Quick start: SKILLS install

This is the recommended starting point.

```bash
npx -y skills add beyondeth/codebase-skills \
  --skill codebase-skill \
  -a codex -a claude-code -a gemini-cli -a antigravity \
  -g -y
```

If you want a single agent only:

```bash
npx -y skills add beyondeth/codebase-skills --skill codebase-skill -a codex -g -y
npx -y skills add beyondeth/codebase-skills --skill codebase-skill -a claude-code -g -y
npx -y skills add beyondeth/codebase-skills --skill codebase-skill -a gemini-cli -g -y
npx -y skills add beyondeth/codebase-skills --skill codebase-skill -a antigravity -g -y
```

Verify installation:

```bash
npx -y skills list -g -a codex -a claude-code -a gemini-cli -a antigravity
```

If `codebase-skill` appears, installation is complete.

Important:

- `SKILLS install` does not mean “your API key is already configured”.
- It means the workflow docs, style guides, and routing rules are now installed for your agent.

## MCP direct setup

If you want to connect MCP manually, read these docs:

- Korean install guide: [docs/guide/installation.md](./docs/guide/installation.md)
- English install guide: [docs/guide/installation.en.md](./docs/guide/installation.en.md)

Create API keys at: `https://codebase.blog/settings/api-keys`

## First-use workflow

When the user actually starts auto-posting, the normal flow is:

1. the agent chooses the installed skill route or MCP route
2. authentication is verified
3. a writing style is selected
4. the post is drafted from that style guide
5. the post is published with `create_post`

So this package is not just “files to install”.  
It is a consistent workflow bundle for `auth -> style -> writing -> publish`.

## Why writing styles matter

A writing style is not just a label for tone. It also affects:

- the post structure
- the voice and rhythm
- what kind of evidence should be included
- who the writing is for
- how the final article should read

Examples:

- `default` is the safest all-purpose technical blog format
- `pm` is for product strategy, decisions, and trade-offs
- `research` is for evidence, experiments, limitations, and analysis
- `marketer` is for growth experiments, conversion insights, and messaging
- `designer` is for UX reasoning and design case studies

Detailed style explanations are available here:

- Style guide details (English): [docs/guide/writing-styles.en.md](./docs/guide/writing-styles.en.md)
- 스타일 가이드 상세(한국어): [docs/guide/writing-styles.md](./docs/guide/writing-styles.md)
- Actual bundled style files: [skills/codebase-skill/writing-styles](./skills/codebase-skill/writing-styles)

If the user is unsure, start with `default`.

## The actual style files are included

This package includes the real markdown files used as writing style sources.

Included files:

- `_common.md`
- `default.md`
- `novel.md`
- `podcast.md`
- `vibe.md`
- `research.md`
- `pm.md`
- `designer.md`
- `marketer.md`

That means users are not limited to a short style name.  
They can open the actual files and inspect the writing rules directly.

## Custom styles are supported

If a user wants their own voice, banned phrases, structure rules, or examples, they can use a custom style file instead of a built-in preset.

Starting file:

- [custom-template.md](./skills/codebase-skill/writing-styles/custom-template.md)

Recommended flow:

1. copy `custom-template.md`
2. fill in tone, structure, banned phrases, and example paragraphs
3. let the agent read that file
4. the agent passes it to MCP as `customMarkdown`
5. the final post is drafted and published from that guide

The MCP server already supports `customMarkdown` and `styleAlias`, so a user-authored style file can become the source of truth for auto-posting.

## LLM agents guide

If you want an agent to guide installation step by step, give it this raw guide:

```bash
curl -s https://raw.githubusercontent.com/beyondeth/codebase-skills/refs/heads/main/docs/guide/installation.md
```

## Update / remove

```bash
npx -y skills check
npx -y skills update
npx -y skills remove codebase-skill -a codex -a claude-code -a gemini-cli -a antigravity -g -y
```

Notes:

- `-g` means global install
- without `-g`, install applies to the current project only

## Documentation links

- Korean install guide: [docs/guide/installation.md](./docs/guide/installation.md)
- English install guide: [docs/guide/installation.en.md](./docs/guide/installation.en.md)
- Korean style guide: [docs/guide/writing-styles.md](./docs/guide/writing-styles.md)
- English style guide: [docs/guide/writing-styles.en.md](./docs/guide/writing-styles.en.md)
- Main skill doc: [skills/codebase-skill/SKILL.md](./skills/codebase-skill/SKILL.md)
- MCPorter cheat sheet: [skills/codebase-skill/MCPORTER_SKILL.md](./skills/codebase-skill/MCPORTER_SKILL.md)

## Layout

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
