---
name: codebase-skill
description: "Codebase.blog auto-posting via MCPorter + OAuth. Trigger words: 자동포스팅, 자동포스팅해, 포스팅해줘, 블로그 포스팅해줘, 글 발행해줘, create post, publish post. Route rule: skill로 -> mcporter (/mcp-remote), mcp로 -> direct MCP (/mcp), ambiguous defaults to skill."
---

# Codebase.blog Auto-Posting (MCP + MCPorter)

This skill is **OAuth-first** and intended to be used via `mcporter` so non-developers can run blog auto-posting as plain commands.

## What This Skill Does

- Authenticate once via OAuth (browser)
- Call MCP tools like normal commands
- Publish posts with `create_post`
- Optional image upload via presigned URL (`get_image_upload_url` -> `curl PUT` -> `finalize_uploaded_image`)

## Trigger Phrases

- 자동포스팅
- 자동포스팅해
- 포스팅해줘
- 블로그 포스팅해줘
- 글 발행해줘
- create post
- publish post

## Routing Contract (Skill vs MCP Direct)

Use explicit user intent to choose one execution path. Do not mix both in one run.

### Route Selection

- `skill` route (via `mcporter`): if user says `codebase-skill`, `skill 사용`, `skill로`, `스킬로`, or uses style flags like `--podcast`, `--research`, `--pm`.
- `mcp` route (direct MCP tools): if user says `mcp로`, `MCP tool`, `codebase-blog-mcp`, `툴로 직접`.
- ambiguous phrase only (for example: `자동포스팅해`): default to `skill` route.
- user can always override by adding one explicit token: `skill로` or `mcp로`.

### Route Guard

Before `create_post`, always run `check_auth` and validate the expected auth mode:

- `skill` route expected output: `인증 방식 : OAuth 2.1`
- `mcp` route expected output: `인증 방식 : API Key`

If mismatch:

1. retry once on the correct route
2. if still mismatched, stop and report route mismatch (do not post)

### Preflight Log Line (required)

Print one route line before tool execution:

- skill route: `[Route] mode=skill transport=mcporter endpoint=/mcp-remote alias=codebase-blog-oauth`
- mcp route: `[Route] mode=mcp transport=direct endpoint=/mcp server=codebase-blog-mcp`

## Setup (Once)

```bash
# PROD (DEFAULT for this skill)
# - User-facing default. Most users should configure this alias only.
npx -y mcporter config add codebase-blog-oauth \
  --url https://mcp.codebase.blog/mcp-remote \
  --auth oauth \
  --oauth-redirect-url http://127.0.0.1:33333/callback \
  --scope home

# DEV (local testing only)
# - Use this only if you are running the local MCP proxy on port 3002.
npx -y mcporter config add codebase-blog-oauth-dev \
  --url http://localhost:3002/mcp-remote \
  --auth oauth \
  --allow-http \
  --oauth-redirect-url http://127.0.0.1:33334/callback \
  --scope project

# Browser OAuth (first time only)
npx -y mcporter auth codebase-blog-oauth
```

## Writing Styles (Plain Language)

Writing style means the overall tone and structure the AI will follow when drafting the post.

- `default`: 가장 무난한 기본형 기술 글
- `novel`: 이야기처럼 읽히는 서사형 글
- `podcast`: 대화하듯 쉽게 풀어쓰는 글
- `vibe`: 개발 성장과 학습 조언 중심 글
- `research`: 근거, 실험, 한계를 엄격히 다루는 글
- `pm`: 제품 의사결정과 전략 설명에 맞는 글
- `designer`: UX 맥락과 디자인 판단을 설명하는 글
- `marketer`: 성장, 실험, 전환 중심 글

Actual preset files are included in this package:

- `writing-styles/_common.md`
- `writing-styles/default.md`
- `writing-styles/novel.md`
- `writing-styles/podcast.md`
- `writing-styles/vibe.md`
- `writing-styles/research.md`
- `writing-styles/pm.md`
- `writing-styles/designer.md`
- `writing-styles/marketer.md`

If the user does not know which one to choose, start with `default`.

## Custom Writing Styles

Users can also create their own style markdown file and use that as the source of truth.

Recommended starting point:

- `writing-styles/custom-template.md`

Recommended flow:

1. User copies `custom-template.md`
2. User edits the file with their own tone, structure, forbidden phrases, and examples
3. The agent reads that file
4. The agent calls `get_writing_style_guide(customMarkdown: "...", styleAlias: "custom-name")`
5. The agent writes the post from that returned guide
6. The agent calls `create_post(..., writingStyle: "custom:custom-name")`

If a custom style file exists, prefer it over built-in presets.

## Verify (Always First)

> Important: treat `check_auth` as the real success gate. Do not rely on the browser page text alone.

```bash
npx -y mcporter call codebase-blog-oauth.check_auth
```

## Safe Gate (Recommended)

`mcporter` may print errors without a non-zero exit code. Gate on the presence of `"error"` in the output before posting.

```bash
AUTH_OUT=$(npx -y mcporter call codebase-blog-oauth.check_auth --output json 2>&1 || true)
echo "$AUTH_OUT"

if echo "$AUTH_OUT" | grep -q '"error"'; then
  echo "[STOP] OAuth verification failed. create_post not executed."
  exit 1
fi
```

## Publish

```bash
npx -y mcporter call 'codebase-blog-oauth.create_post(
  title: "자동포스팅 테스트",
  content_markdown: "## Hello\\n\\nmcporter로 발행한 글입니다.",
  category: "Tech",
  tags: ["mcp","mcporter","automation"]
)'
```

## Writing Style Guide (Optional)

```bash
npx -y mcporter call 'codebase-blog-oauth.get_writing_style_guide(style: "default")'
```

## Image Upload (Optional)

```bash
# 1) ask for presigned URL
npx -y mcporter call 'codebase-blog-oauth.get_image_upload_url(mimeType: "image/webp", fileSize: 245760)'

# 2) upload with curl PUT (use uploadUrl from step 1)
curl -X PUT -H "Content-Type: image/webp" -T ./cover.webp "UPLOAD_URL_FROM_PREVIOUS_STEP"

# 3) finalize upload
npx -y mcporter call 'codebase-blog-oauth.finalize_uploaded_image(fileKey: "uploads/...", mimeType: "image/webp", fileSize: 245760)'
```

## Troubleshooting

- If the login UI does not appear: you may already be logged in. Try a private window or `npx -y mcporter auth codebase-blog-oauth --reset`.
- If you see `SSE error: Invalid content type, expected "text/event-stream"` during `mcporter auth`: tokens may still be saved. Run `check_auth` to confirm.
- If port `33333` is in use: pick another fixed callback port and re-add the production alias.
- If you want to test locally, authenticate the dev alias separately: `npx -y mcporter auth codebase-blog-oauth-dev`.
