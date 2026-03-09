# codebase-skills

Codebase.blog is a platform that turns conversations and work with AI agents into blog posts.  
Install `codebase-skill` to use auto-posting more easily in Codex, Claude Code, Gemini CLI, and Antigravity.

Korean version: [README.md](./README.md)

Supported agents:

- `codex`
- `claude-code`
- `gemini-cli`
- `antigravity`

## Easiest install

Most users should start with `SKILLS install`.

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

## Other install paths

- Install path chooser: [docs/guide/installation.en.md](./docs/guide/installation.en.md)
- `SKILLS install` guide: [docs/guide/skills-installation.en.md](./docs/guide/skills-installation.en.md)
- `MCP direct` guide: [docs/guide/mcp-direct.en.md](./docs/guide/mcp-direct.en.md)

Create API keys at:

- `https://codebase.blog/settings/api-keys`

## Writing styles

This skill includes the real markdown writing style files.  
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

## Custom styles

- `_common.md`
- `default.md`
- `novel.md`
- `podcast.md`
- `vibe.md`
- `research.md`
- `pm.md`
- `designer.md`
- `marketer.md`

If you already have a brand voice, banned phrases, or title rules, use a custom style file instead of a preset.

Starting file:

- [custom-template.md](./skills/codebase-skill/writing-styles/custom-template.md)

Recommended flow:

1. Copy `custom-template.md`
2. Fill in tone, structure, banned phrases, and example paragraphs
3. Let the agent read that file
4. The agent passes it to MCP as `customMarkdown`
5. The post is drafted and published from that guide

The MCP server already supports `customMarkdown` and `styleAlias`.  
That means a user-authored style file can become the actual source of truth for auto-posting.

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
