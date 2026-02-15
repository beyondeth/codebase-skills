---
name: codebase-blog-mcporter
version: 1.0.0
description: Command-first skill for 5-tool codebase-blog MCP publishing via mcporter. Triggers: 자동포스팅, 자동포스팅해, 포스팅해줘, 블로그 포스팅해줘, 글 발행해줘, create post, publish post.
---

# Codebase Blog MCPorter Skill

## Trigger Phrases (for auto-selection)

- 자동포스팅
- 자동포스팅해
- 포스팅해줘
- 블로그 포스팅해줘
- 글 발행해줘
- create post
- publish post

## Selection Rule

- 사용자가 위 트리거 문구로 발행 의도를 말하면, 이 스킬의 `mcporter` 명령 흐름을 우선 사용합니다.
- 이미 MCP 서버가 연결되어 있어도, 사용자 발화가 “자동포스팅/포스팅해줘” 계열이면 먼저 `check_auth` 후 발행 절차를 진행합니다.

`mcporter`를 사용해서 `codebase-blog-mcp`를 일반 명령어처럼 호출하는 가이드입니다.

## 1) 초기 1회 설정 (권장: OAuth)

```bash
# PROD (일반 사용자)
npx -y mcporter config add codebase-blog-oauth --url https://mcp.codebase.blog/mcp-remote --auth oauth --oauth-redirect-url http://127.0.0.1:33333/callback --scope home

# DEV (테스트용)
npx -y mcporter config add codebase-blog-oauth-dev --url http://localhost:3002/mcp-remote --auth oauth --allow-http --oauth-redirect-url http://127.0.0.1:33334/callback --scope project

# 브라우저 인증 (초기 1회)
npx -y mcporter auth codebase-blog-oauth
```

## 2) 5-tool 기본 명령

```bash
# 도구 스키마 확인
npx -y mcporter list codebase-blog-oauth --schema

# 인증 확인 (권장: 항상 먼저)
npx -y mcporter call codebase-blog-oauth.check_auth

# 스타일 가이드 조회
npx -y mcporter call 'codebase-blog-oauth.get_writing_style_guide(style: "default")'

# 이미지 업로드 1단계 (선택)
npx -y mcporter call 'codebase-blog-oauth.get_image_upload_url(mimeType: "image/webp", fileSize: 245760)'

# 응답의 uploadUrl로 PUT 업로드 (로컬 파일)
curl -X PUT -H "Content-Type: image/webp" -T ./cover.webp "UPLOAD_URL_FROM_PREVIOUS_STEP"

# 이미지 업로드 2단계 (선택)
npx -y mcporter call 'codebase-blog-oauth.finalize_uploaded_image(fileKey: "uploads/...", mimeType: "image/webp", fileSize: 245760)'

# 포스트 생성
npx -y mcporter call 'codebase-blog-oauth.create_post(title: "MCP 자동포스팅 예시", content_markdown: "# Hello\n\nmcporter로 발행한 글입니다.", category: "Tech", tags: ["mcp","automation"])'
```

## 2-1) 로그인 성공 확인 후 바로 자동포스팅 (연속 실행 예시)

```bash
npx -y mcporter auth codebase-blog-oauth --reset && \
npx -y mcporter call codebase-blog-oauth.check_auth && \
npx -y mcporter call 'codebase-blog-oauth.create_post(title: "[테스트] OAuth 자동포스팅", content_markdown: "# OAuth E2E\\n\\n로그인 성공 후 자동포스팅 테스트입니다.", category: "Tech", tags: ["oauth","test"])'
```

## 2-2) 안전 게이트 (권장)

`mcporter`는 일부 오류 케이스에서 종료코드가 0일 수 있으므로, `check_auth` 결과에 `"error"`가 있는지 확인한 뒤에만 발행합니다.

```bash
AUTH_OUT=$(npx -y mcporter call codebase-blog-oauth.check_auth --output json 2>&1 || true)
echo "$AUTH_OUT"

if echo "$AUTH_OUT" | rg -q '"error"'; then
  echo "[STOP] OAuth verification failed. create_post not executed."
  exit 1
fi

npx -y mcporter call 'codebase-blog-oauth.create_post(title: "OAuth 게이트 통과 후 발행", content_markdown: "## Hello\n\ncheck_auth 성공 후 발행 테스트입니다.", category: "Tech", tags: ["oauth","gate"])'
```

## 3) API Key 모드가 필요한 경우 (선택)

```bash
export CODEBASE_MCP_TOKEN="blog_sk_..."
npx -y mcporter config add codebase-blog-mcp --url https://mcp.codebase.blog/mcp --header "Authorization=Bearer ${CODEBASE_MCP_TOKEN}" --header "Accept=application/json, text/event-stream" --scope home
npx -y mcporter call codebase-blog-mcp.check_auth
```

## 4) 실패 시 점검

- `401 Unauthorized`: OAuth 재인증(`mcporter auth codebase-blog-oauth`) 또는 API Key 값 확인
- `offline` 또는 timeout: 네트워크/VPN/방화벽 확인
- OAuth 로그인 화면이 안 보이면: 이미 로그인 세션이 살아있을 수 있음. 시크릿 창 또는 `mcporter auth ... --reset`으로 재시도
- 이미지 업로드 실패: 업로드 단계 중단 후 `create_post`를 텍스트-only로 진행

## 5) 보안 규칙

- 기본은 OAuth를 사용하고, API Key가 필요할 때만 환경 변수에 보관합니다.
- 운영 환경에서는 키를 주기적으로 재발급합니다.
- 공개 저장소에 `mcporter` 설정 파일을 커밋하지 않습니다.
