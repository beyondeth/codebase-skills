# codebase-skills

Skill package for connecting Codebase.blog auto-posting to AI agents.  
The goal is simple: make the install path clear and keep the `auth -> style -> writing -> publish` workflow consistent.

Korean version: [README.md](./README.md)

## Who is this for?

- users who want Codebase.blog auto-posting
- users who are new to MCP setup
- users who want both style explanations and the real markdown style files
- users who want to publish from their own custom style files

Supported agents:

- `codex`
- `claude-code`
- `gemini-cli`
- `antigravity`

## Choose one install path first

`SKILLS install` and `MCP direct` are different paths. Do not mix them on your first setup.

| Path | Best for | What it gives you |
| --- | --- | --- |
| `SKILLS install` | most users | easiest setup, plus workflow docs and writing styles |
| `MCP direct` | advanced users | direct control over API keys, MCP config, and security policy |

- Start with `SKILLS install` if you want the easiest path
- Use `MCP direct` only if you want to manage the MCP connection yourself

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

## What actually gets installed?

- the auto-posting workflow docs
- MCPorter + OAuth usage guide
- the real markdown writing style files
- a custom style template

So this package is not just a command snippet.  
It installs the workflow docs and style sources that help the agent use Codebase.blog correctly.

## Installation guides

- Install path chooser: [docs/guide/installation.en.md](./docs/guide/installation.en.md)
- `SKILLS install` guide: [docs/guide/skills-installation.en.md](./docs/guide/skills-installation.en.md)
- `MCP direct` guide: [docs/guide/mcp-direct.en.md](./docs/guide/mcp-direct.en.md)

Create API keys at:

- `https://codebase.blog/settings/api-keys`

## Why writing styles matter

A writing style does more than change tone. It also shapes:

- post structure
- sentence rhythm
- what evidence to include
- who the post is written for
- whether the final article reads like product writing, analysis, or explanation

If you are unsure, start with `default`.

Quick recommendations:

| Style | Best for |
| --- | --- |
| `default` | safest all-purpose technical or product post |
| `pm` | product strategy, decisions, and trade-offs |
| `research` | evidence, experiments, analysis, and limitations |
| `marketer` | growth tests, conversion insights, and messaging |
| `designer` | UX reasoning, interface changes, and design case studies |

Style details:

- English: [docs/guide/writing-styles.en.md](./docs/guide/writing-styles.en.md)
- 한국어: [docs/guide/writing-styles.md](./docs/guide/writing-styles.md)
- Actual bundled files: [skills/codebase-skill/writing-styles](./skills/codebase-skill/writing-styles)

## The actual style files are included

This package ships with the real markdown files used as writing style sources.

- `_common.md`
- `default.md`
- `novel.md`
- `podcast.md`
- `vibe.md`
- `research.md`
- `pm.md`
- `designer.md`
- `marketer.md`

That means users are not limited to short preset names.  
They can open the actual files and inspect the writing rules directly.

## Custom styles are supported

If you already have a brand voice, banned phrases, section rules, or title rules, a custom style file is often better than a preset.

Starting file:

- [custom-template.md](./skills/codebase-skill/writing-styles/custom-template.md)

Recommended flow:

1. Copy `custom-template.md`
2. Fill in tone, structure, banned phrases, and example paragraphs
3. Let the agent read that file
4. The agent passes it to MCP as `customMarkdown`
5. The post is drafted and published from that guide

The MCP server already supports `customMarkdown` and `styleAlias`, so a user-authored style file can become the actual source of truth for auto-posting.

## If you want an LLM agent to guide installation

Give the agent this raw guide and let it walk through the setup step by step:

```bash
curl -s https://raw.githubusercontent.com/beyondeth/codebase-skills/refs/heads/main/docs/guide/installation.en.md
```

## Update / remove

```bash
npx -y skills check
npx -y skills update
npx -y skills remove codebase-skill -a codex -a claude-code -a gemini-cli -a antigravity -g -y
```

Notes:

- `-g` means global install
- without `-g`, installation applies to the current project only

## Read next

- Korean install path chooser: [docs/guide/installation.md](./docs/guide/installation.md)
- English install path chooser: [docs/guide/installation.en.md](./docs/guide/installation.en.md)
- Korean style guide: [docs/guide/writing-styles.md](./docs/guide/writing-styles.md)
- English style guide: [docs/guide/writing-styles.en.md](./docs/guide/writing-styles.en.md)
- Main skill doc: [skills/codebase-skill/SKILL.md](./skills/codebase-skill/SKILL.md)
- MCPorter cheat sheet: [skills/codebase-skill/MCPORTER_SKILL.md](./skills/codebase-skill/MCPORTER_SKILL.md)
