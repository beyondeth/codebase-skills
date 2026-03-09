# Writing Styles Guide

This guide helps users quickly choose the right bundled style in `codebase-skill`.

Actual source files:

- [skills/codebase-skill/writing-styles](../../skills/codebase-skill/writing-styles)

## Best default choice

If you are not sure which style to pick, start with `default`.

Why `default` is the safest first choice:

- it works for most technical and product posts
- it is not too specialized for one role
- it handles both explanation and reflection reasonably well

## How to choose a style

Start with these three questions:

1. What is this post mainly about?
   - implementation, architecture, product decisions, experiments, UX changes
2. Who is the reader?
   - engineers, product team, designers, marketers, general users
3. What should the post feel like?
   - analytical, product-oriented, explanatory, conversational, story-driven

## Quick chooser

| Style | Best for | Tone |
| --- | --- | --- |
| `default` | implementation writeups, feature summaries, technical comparisons | balanced and safe |
| `pm` | product decisions, strategy, priorities, trade-offs | product and decision focused |
| `research` | experiments, evidence, benchmarks, limitations | analytical and strict |
| `marketer` | growth tests, conversion, messaging experiments | persuasion and outcomes |
| `designer` | UX improvements, interface changes, design rationale | context and intent |
| `novel` | incident stories, personal journeys, debugging narratives | story-driven |
| `podcast` | Q&A, easy explanations, spoken-style flow | conversational |
| `vibe` | learning advice, career guidance, mentoring | light and encouraging |

## Style-by-style overview

### `default`

The safest all-purpose technical blog format.

Best for:

- implementation writeups
- architecture explanations
- feature summaries
- technical comparisons

### `pm`

Best for product and strategy writing.

Best for:

- explaining why a feature was built
- documenting why one option was chosen over another
- describing user problems, priorities, and trade-offs

### `research`

Best for evidence-heavy and analytical posts.

Best for:

- paper reviews
- experiment summaries
- benchmark interpretation
- limitations and risk analysis

### `marketer`

Best for growth and conversion-oriented writing.

Best for:

- campaign retrospectives
- conversion analysis
- copy and messaging experiments
- channel performance learnings

### `designer`

Best for design case studies and UX reasoning.

Best for:

- UX improvement writeups
- interface restructuring decisions
- design rationale
- before / after case studies

### `novel`

Best for story-driven writing.

Best for:

- incident stories
- debugging journeys
- experience-driven posts with emotional arc

### `podcast`

Best for conversational writing.

Best for:

- Q&A format
- easy concept explanations
- content that should read like spoken dialogue

### `vibe`

Best for learning and mentoring posts.

Best for:

- learning methods
- career advice
- AI-era study strategy
- mentoring-style developer posts

## When a custom style is better

Use a custom style file when:

- your brand voice is already defined
- you have explicit banned phrases
- you want fixed title or section rules
- you want strong control over structure
- you want example paragraphs to shape the output

Starting file:

- [custom-template.md](../../skills/codebase-skill/writing-styles/custom-template.md)

## Recommended custom-style workflow

1. Copy `custom-template.md`
2. Fill in tone, structure, banned phrases, and example paragraphs
3. Let the agent read that file
4. The agent passes it to MCP as `customMarkdown`
5. The post is drafted from the returned guide
6. The publish step can record it as `custom:<alias>`

In other words, a custom style file is not just a note. It can become the actual source of truth for auto-posting.
