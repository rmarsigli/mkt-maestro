---
name: publish-social-post
description: Publishes an approved social media post (image + caption) to Instagram and Facebook via their Graph API.
---
# Publish Social Post Workflow

When the user asks to publish or post a specific social media post:

1. Identify the `client_id` and the `post_id`.
2. Verify the post status in `clients/<client_id>/posts/<post_id>.json` is `approved`.
3. Locate the associated media file (e.g., `<post_id>.png` or `.mp4`).
4. Read the `brand.json` or a `.env` file to retrieve the Meta App Access Tokens and Page IDs.
5. Create a temporary script using Node.js/Bun in the `ui` folder that:
   - Uploads the media to the Facebook Graph API (e.g., `/me/photos` or `/me/video`).
   - Appends the `content` and `hashtags` from the JSON to the caption.
6. Execute the script via `run_shell_command`.
7. On success, update the local JSON `status` to `published`.
