---
name: deploy-google-ads
description: Deploys an approved Google Ads campaign JSON draft to the live Google Ads API.
---
# Deploy Google Ads Workflow

## Important Notes

- Only campaigns with `status: "approved"` can be deployed.
- `budget_suggestion` is a human-readable string (e.g. `"R$50/dia"`). The script parses it automatically.
- The script creates all assets as **PAUSED** by default — review in the Google Ads UI before enabling.

## Steps

1. Identify `client_id` and the campaign JSON filename.
2. Verify `status: "approved"` in `clients/<client_id>/ads/google/<campaign_id>.json`. Stop if not approved.
3. Confirm `website_url` exists in `clients/<client_id>/brand.json` (required as `final_url`).
4. Show the user what will be deployed: campaign name, ad groups count, budget.
5. Run from the project root:
   ```bash
   bun run scripts/deploy-google-ads.ts clients/<client_id>/ads/google/<campaign_id>.json
   ```
6. On success, the script updates local JSON `status` to `"published"` automatically.
7. On failure, report the full error. Do not retry without understanding the cause.
