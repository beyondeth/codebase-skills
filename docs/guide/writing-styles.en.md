# Writing Styles Guide

This guide explains what each bundled writing style is for and when it should be used.

The actual source files are here:

- [skills/codebase-skill/writing-styles](../../skills/codebase-skill/writing-styles)

## Best default choice

If you are not sure which style to pick, start with `default`.

`default` works well because it is:

- balanced
- technical without being too rigid
- suitable for most product and engineering posts

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
- documenting a product decision
- describing trade-offs, priorities, and user problems

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
- you want a fixed title or section structure
- you want example paragraphs to strongly shape the output

Starting file:

- [custom-template.md](../../skills/codebase-skill/writing-styles/custom-template.md)

## Recommended custom-style workflow

1. Copy `custom-template.md`
2. Fill in tone, structure, banned phrases, and example paragraphs
3. Let the agent read that file
4. The agent passes it as `customMarkdown`
5. The post is drafted from the returned guide
6. The publish step can record it as `custom:<alias>`

In other words, a custom style file is not just a note. It can become the actual source of truth for auto-posting.
