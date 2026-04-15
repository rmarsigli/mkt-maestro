---
name: optimize-roas
description: Analyzes a live Google Ads campaign and automatically pauses underperforming Ad Groups while shifting budget to high-ROAS Ad Groups.
---
# Optimize ROAS Workflow

When the user asks to optimize ROAS or fix a bleeding campaign:

1. Identify the `client_id` and the `campaign_id` (from Google Ads).
2. Fetch the live detailed report using `getDetailedCampaign` from `$lib/server/googleAdsDetailed.ts` (as seen in the `get-google-ads-campaign` skill).
3. Analyze the Ad Groups data:
   - **High Performers:** Ad Groups with Conversions > 0 and ROAS > 200% (or an acceptable CPA).
   - **Low Performers:** Ad Groups with High Cost, High Clicks, but 0 Conversions.
4. Inform the user of your findings (e.g., "Ad Group X spent $50 with 0 conversions. Ad Group Y has a ROAS of 300%.").
5. Propose a plan: "I will pause Ad Group X via the API."
6. Once confirmed by the user, create a temporary script to execute a `MutateOperation` that sets the status of the bleeding Ad Group to `PAUSED`.
7. Run the script and confirm success.
