---
name: deploy-google-ads
description: Deploys an approved Google Ads campaign from a local JSON draft to the live Google Ads API.
---
# Deploy Google Ads Workflow

When the user asks to deploy, launch, or push a specific Google Ads campaign:

1. Identify the `client_id` and the `campaign_id` (the JSON filename).
2. Verify that the campaign status is `approved` in `clients/<client_id>/ads/google/<campaign_id>.json`.
3. If it's not approved, warn the user and stop.
4. Read the `brand.json` to extract `google_ads_id`.
5. Tell the user you are deploying the campaign.
6. Create a temporary deployment script in the `ui` folder that imports `google-ads-api`, parses the local JSON, and creates `MutateOperations` for the Campaign, Budget, and Ad Groups.
7. Execute the script using `bun run`. 
8. On success, update the local JSON `status` from `approved` to `published` and delete the temporary script.
