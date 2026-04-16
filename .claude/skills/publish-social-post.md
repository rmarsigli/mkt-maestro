---
name: publish-social-post
description: Publishes an approved social media post (image + caption) to Instagram and Facebook via the Meta Graph API.
---
# Publish Social Post Workflow

## Required in .env
```
META_PAGE_ACCESS_TOKEN=
META_PAGE_ID=
META_INSTAGRAM_ACCOUNT_ID=
MEDIA_PUBLIC_BASE_URL=   # public URL for media files (ngrok/tunnel)
```

## Steps

1. Identify `client_id` and `post_filename` (e.g. `2025-04-15_lancamento.json`).
2. Verify `status: "approved"` in `clients/<client_id>/posts/<post_filename>`. Stop if not approved.
3. Confirm a media file exists with the same base name (`.png`, `.mp4`, etc.).
4. Run from the project root:
   ```bash
   bun run scripts/publish-social-post.ts <client_id> <post_filename>
   ```
5. The script handles: container creation → polling for FINISHED → publish → status update to `"published"`.
6. On failure, report the full error. Do not retry without diagnosing the cause.
