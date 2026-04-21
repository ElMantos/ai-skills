---
name: meta-ads-ui
description: Operate the Meta Ads Manager UI (business.facebook.com / adsmanager.facebook.com) on behalf of the user — validating that ads are actually running, publishing drafts correctly, duplicating ad sets across markets or regions, and navigating the campaign / ad set / ad hierarchy without falling into common publish-scope traps. Use whenever the user asks you to "check my ad", "make sure my ad is running", "publish my ad", "why is my ad still a draft", "copy my ad for Germany", "duplicate this for another country", "run this in a new market", or any hands-on task that involves clicking through Ads Manager itself (as opposed to writing ad copy or debugging billing). Also trigger after any ad creation, edit, or duplication flow to verify delivery status before reporting back. This is the skill for actually operating the UI; pair with meta-ads-debugger when delivery is clearly broken, or with instagram-ads for creative and strategy work.
---

# Meta Ads Manager UI Skill

A skill for operating the Meta Ads Manager interface on the user's behalf. Use when you need to verify, edit, or publish something in Ads Manager — not when you're writing copy or debugging billing (other skills cover those).

## Prerequisite

The user needs a browser open and logged into Meta Ads Manager (business.facebook.com/adsmanager or adsmanager.facebook.com). If they aren't, ask them to open it and share their screen before you start clicking around.

## The three-level hierarchy (and why it matters)

Meta Ads are nested three levels deep. Almost every confusing issue traces back to operating at the wrong level.

- **Campaign** — top level. Holds the objective and, for CBO campaigns, the overall budget.
- **Ad Set** — middle level. Holds targeting (audience, geo, age), placements, schedule, and ad-set budget.
- **Ad** — bottom level. The actual creative, copy, and destination link.

An ad only serves impressions when every level above it is simultaneously: toggled on, fully published (no drafts), and free of policy errors. If any single level is off, in draft, or rejected, the ad does not run — regardless of what the upper levels look like.

## Workflow: Validate that an ad is actually running

This is the default verification pass. Run it after any publish, any edit, or whenever the user asks "is my ad running?" — and also proactively after you've just done something that was supposed to make an ad run.

Always validate from the ad level, not the campaign level. The campaign-level "Active" light is misleading: it only says the campaign is switched on, not that any ad underneath it is delivering.

1. **Open the ad set's ads view.** In Ads Manager, select the campaign in the Campaigns table → click the "Ads" tab at the top of the data table. You should see the actual ad row with its Delivery column populated.

2. **Read the Delivery column for the ad.** This is the single source of truth.
   - `Active` — the ad is serving impressions. You're done; report back "✓ running".
   - `Processing` — Meta is still reviewing the creative. Also fine — review usually clears within a few hours. Confirm the ad set's end date hasn't already passed, then report back "✓ in review, will start serving once approved".
   - `Draft` — the ad has unpublished changes. Go to the Publish section below.
   - `Not delivering`, `Delivery error`, `Rejected`, `In review` stuck >48h — the ad has a problem. Go to the Debug section below.
   - `Paused`, `Off` — the on/off toggle is off. See step 3.

3. **Check the on/off toggle on the ad row.** A published, approved ad with its toggle off will still not deliver. If the toggle is off, ask the user whether to turn it on before doing so — don't flip it silently.

4. **Sanity-check the ad set's end date.** If the schedule already ended, the ad won't deliver regardless of status. Note this and surface it to the user if relevant.

## Debug: Ad is in an error state

When Delivery shows an error or rejection, don't guess — read the exact message.

1. Click into the ad name to open its edit panel.
2. Click the **Review** tab at the top of the editor. Any rejection or policy violation is listed there verbatim with a policy code (e.g., `#3843078`).
3. Report the exact message back to the user in plain language. Common patterns:
   - *"Promote Ads Without Organic Media"* — the Instagram post backing the boost is deleted, unpublished, or had its original media changed. Fix: re-boost from an intact post.
   - *"In review"* stuck for >48 hours — contact Meta support via Help Center.
   - Audience-too-small warnings — broaden targeting in the ad set.

4. If the skill `meta-ads-debugger` is available and the issue looks account-wide (billing, restrictions, no delivery across multiple ads), hand off to it for a full diagnostic rather than debugging inline.

## Publish: ad set ≠ ad

Internalize this, because the user gets tripped up here constantly: **publishing at the ad set level does not reliably cascade to nested ad drafts.** If someone edits an ad, hits "Publish" from inside the ad set editor, and then wonders why the ad still says `Draft` — this is exactly why. The publish scope follows where you clicked the button, not where the draft lives.

Two reliable paths to publish ad-level changes:

1. **Top-right "Review and publish" button** in Ads Manager. This surfaces every pending change across campaigns, ad sets, and ads, and publishes them together. Use this when in doubt — it's the belt-and-suspenders option.

2. **Drill into the ad itself** (Campaigns → Ads tab → click the ad → Edit) and click **Publish** at the bottom of that ad's editor. This publishes only that ad but guarantees ad-level drafts get pushed.

The rule to follow after any publish action: go back to the ad level and re-read its Delivery status. If it still says `Draft` or the "Review and publish" button is still highlighted at the top right, the publish didn't include the ad — redo it via path 1 or path 2 above.

Always ask the user before clicking Publish. The Publish button is irreversible in the sense that it commits the ad to Meta's delivery system; even though you can pause later, you shouldn't treat it as a safe default click.

## Workflow: Duplicate an ad for a new market or region

When the user wants to run the same creative in a different country, region, or audience segment (e.g., "copy this ad for Germany", "run it in the US too", "duplicate for DACH", "expand to Nordics"), the right level to duplicate is almost always the **ad set** — not the ad and not the campaign. Here's why:

- Geographic and audience targeting live at the ad set level. Duplicating just the ad gives you two ads pointing at the same audience — pointless for market expansion.
- Duplicating the campaign creates a whole parallel campaign with its own budget and objective. That fragments reporting and usually creates more separation than the user actually wants.
- Duplicating the ad set is the sweet spot: Meta automatically copies every ad inside it, so the creative carries over, and you get a fresh targeting container to point at the new market.

Steps:

1. In the Ad sets tab (filtered to the relevant campaign), select the source ad set.
2. Click **Duplicate** in the toolbar above the table (or use the row's "⋯" menu). When Meta asks whether to create the duplicate under the original campaign or a new one, choose **"Original campaign"** unless the user explicitly wants a separate campaign — staying in the same campaign keeps reporting and budget logic unified.
3. In the draft ad set that opens, change only what needs to change: almost always the geographic targeting and the name. Sometimes the budget, if it should differ per market. Leave creative, placements, optimization, and everything else alone unless the user asks.
4. Before saving, confirm with the user: "I'll name this `<proposed name>` targeting `<new geo>` — OK?" (see the Naming section below).
5. Verify the ads copied over: open the new ad set's Ads tab and confirm the same creatives are present with `Draft` status.
6. Follow the publish + validate flow in the sections above. The publish scope trap applies doubly here — the duplicated ads are new ad-level drafts and often don't get pushed live by an ad-set-level publish. Use "Review and publish" at the top right, then re-check each new ad's Delivery status to confirm.

## Naming: match the established pattern and verify before saving

Whenever you're creating or duplicating an ad set or ad, look at the existing names already in the account and match the same pattern, changing only the tokens that genuinely differ. Then — this is the important part — show the user the proposed name and ask them to confirm before you save it. Don't invent names silently.

How to extract the pattern:

1. Read the source ad set's (or ad's) name. Break it into tokens separated by ` - `, `_`, or `|` — whatever the user's convention is.
2. Identify which token describes the thing you're changing. For market duplication it's almost always the geo token (e.g., `USA/CA`, `DE`, `EU`). For audience variation it might be the age or interest token.
3. Swap only that token. Leave everything else intact, including dates, product names, version numbers, and the separator style.

Example:

- Source ad set: `Collagen - USA/CA - Women 30-55 - Apr26`
- User asks: "duplicate for Germany and Denmark"
- Propose: `Collagen - DE/DK - Women 30-55 - Apr26`
- Ask user: "Use `Collagen - DE/DK - Women 30-55 - Apr26` as the name? (Happy to adjust.)"

If the source name has no visible pattern (single word, unclear tokens), don't guess silently — propose a pattern explicitly, explain the tokens you're introducing, and let the user sign off before you standardize.

Why this matters: Ads Manager reports are filtered and compared by name. Inconsistent naming makes it impossible to answer questions like "how did the Collagen product perform in DACH versus North America?" a week later. A minute of naming alignment up front saves hours of retroactive renaming.

## Navigation tips

- Campaigns URL pattern: `https://adsmanager.facebook.com/adsmanager/manage/campaigns?act=<AD_ACCOUNT_ID>`
- Billing URL pattern: `https://business.facebook.com/billing_hub/payment_settings?asset_id=<AD_ACCOUNT_ID>`
- Switch between Campaigns / Ad sets / Ads views using the three tabs right above the data table — not the left sidebar, which is for switching workspaces.
- Selecting a row in a higher tab filters the lower tabs to just that item's children. This is how you drill into a specific campaign's ad sets or ads.
- The green dot on "Delivery" and the on/off toggle mean different things. Toggle = "user wants this on". Delivery = "it is actually serving". Trust Delivery.

## Action safety

- Safe to do without asking: read any status, error message, delivery column, billing screen, or Review tab. Click "See why" / "Learn more" links. Hover elements to reveal tooltips.
- Ask the user first before: toggling any ad, ad set, or campaign on/off. Clicking Publish. Editing budget, schedule, targeting, or creative. Discarding drafts. Adding payment methods.
- Never do: delete campaigns, ad sets, or ads. Accept Terms / Conditions / new policies on the user's behalf. Enter payment card details. Modify account permissions.
