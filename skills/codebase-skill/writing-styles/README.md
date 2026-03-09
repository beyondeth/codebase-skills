# Writing Styles

These are the actual markdown style guides bundled with `codebase-skill`.

## Recommended starting point

- If you are not sure, use `default`.

## Presets

- `default`: balanced technical blog post
- `novel`: story-driven narrative
- `podcast`: conversational dialogue format
- `vibe`: developer learning and mentoring tone
- `research`: evidence-first analysis
- `pm`: product strategy and decision rationale
- `designer`: design case study and UX reasoning
- `marketer`: growth and performance storytelling

## Custom style

If you want your own writing voice:

1. Copy `custom-template.md`
2. Fill in your own tone, structure, banned phrases, and examples
3. Ask the agent to use that file as the style source

The MCP workflow supports:

- `get_writing_style_guide(customMarkdown: "...", styleAlias: "...")`
- `create_post(writingStyle: "custom:<alias>")`

That means user-authored style files can become the source of truth for auto-posting.
