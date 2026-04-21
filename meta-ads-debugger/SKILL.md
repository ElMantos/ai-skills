---
name: meta-ads-debugger
description: >
  Debug Meta / Instagram ad delivery and payment issues using the Ads Manager UI in a browser.
  Use this skill whenever the user has an ad showing as "Active" but with $0 or €0 spend, zero
  impressions, zero delivery, or payment-related problems in Meta Ads Manager or Instagram Boost.
  Also trigger for: billing account issues, payment method errors, ad account flags, prepaid
  balance not spending, boosted posts not delivering, or any "my ad isn't working" complaint
  related to Meta or Instagram advertising. This skill navigates the Ads Manager UI directly —
  the user must have a browser open and be logged into Meta Ads Manager or be willing to open it.
compatibility: "Requires Claude Cowork with browser/screen control (computer_use)"
---

# Meta Ads Debugger Skill

A Cowork skill that navigates Meta Ads Manager in the browser to diagnose why an ad isn't
spending or delivering, explains the root cause clearly, and attempts to fix it where possible.

---

## Prerequisites

Before starting, confirm with the user:
1. They are logged into Meta Ads Manager at **business.facebook.com/adsmanager** (or can open it)
2. The ad account in question is selected
3. Screen sharing / Cowork desktop access is active

If not, ask them to open the URL and share their screen before proceeding.

---

## Diagnostic Checklist (run in this order)

Work through each section systematically. Screenshot or read each screen before clicking further.
After completing all checks, produce a **Diagnosis Report** (see format below).

---

### CHECK 1 — Ad Account Status
**Navigate to**: Ads Manager home → look for any banner warnings at the top of the page.

Look for:
- 🔴 "Your account has been disabled"
- 🟡 "Your account is restricted" or "Limited"
- 🟡 "Payment failed" or "Payment needed"
- 🟡 "Identity verification required"
- Any red or yellow warning banners

**If account is disabled or restricted**: Stop here, report this as the root cause. The user
needs to appeal via the Help Center — this cannot be fixed by clicking around.

---

### CHECK 2 — Payment Method Status
**Navigate to**: Ads Manager → Billing (left sidebar or top menu) → Payment Settings

Look for:
- Is there a primary payment method listed?
- Does it show a green checkmark or a red/yellow warning icon?
- Is there a "Prepaid balance" shown? What is the amount?
- Is there a backup payment method (credit/debit card)?
- Any "Verify payment method" or "Confirm card" prompts

**Common issues to flag**:
- Prepaid balance exists but NO backup card → Meta often requires a card even with balance
- Payment method shows warning icon → click it to read the specific error
- Balance is €0.00 despite user adding funds → funds may be pending or in wrong currency

**If there's a "Verify" or "Confirm" button visible**: Click it and walk the user through
completing verification. This is safe to do.

---

### CHECK 3 — Account Spending Limit
**Navigate to**: Billing → Payment Settings → scroll to "Account Spending Limit"

Look for:
- Is a spending limit set? What is the value?
- Is the current spend near or at the limit?
- Is the limit set to $0 or €0? (This fully blocks all delivery)

**If limit is $0 or blocking spend**: Note this as a likely fix — advise user to remove or
raise the limit. Ask permission before clicking "Edit" to change it.

---

### CHECK 4 — Campaign / Ad Set Status
**Navigate to**: Ads Manager → Campaigns tab

Look for the specific campaign containing the boosted post:
- Campaign status: Active / Paused / In Review / Rejected?
- Ad Set status: Active / Paused / In Review?
- Ad status: Active / Rejected / In Review?

**If any level shows "In Review"**: Normal for new ads — can take 24–48hrs. Note the date
the ad was submitted.

**If any level shows "Rejected"**: Click into it and read the rejection reason. Report the
exact reason to the user.

**If all show "Active" but spend is $0**: Proceed to Check 5.

---

### CHECK 5 — Delivery Insights
**Navigate to**: Click into the Ad Set → look for "Delivery" column → click the chart icon
or "See Delivery Insights" if available.

Look for:
- Audience size estimate — is it above 1,000 people? (Too small = no delivery)
- Any "Limited" labels on delivery
- Bid strategy — is there a bid cap set too low?
- Schedule — is the flight dates correct? Has the end date already passed?

**Also check the Ad Set**: Click into it and verify:
- Start date and end date
- Daily or lifetime budget amount
- Geographic targeting (confirm Germany/Denmark or whatever was set)

---

### CHECK 6 — Billing Activity / Transaction Log
**Navigate to**: Billing → Billing & Payments → Transaction History (or Payment Activity)

Look for:
- Any successful charges (even small ones like €0.01 test charge)
- Any failed payment attempts with error codes
- Whether the prepaid balance shows as "Available" or "Pending"
- Currency of the account vs currency of the payment method

---

## After All Checks — Produce Diagnosis Report

Once you've completed the checks, present a clear report to the user:

```
## Meta Ads Diagnosis Report

**Root Cause(s) Found:**
[List each issue discovered, in plain language]

**What This Means:**
[Explain why this is preventing delivery/spend]

**What I Can Fix Now:**
[List any fixes you can attempt with a click — e.g. "Remove the $0 spending limit"]

**What You Need To Do Manually:**
[List anything that requires the user's action — e.g. "Add a credit card as backup payment"]

**Expected Outcome After Fix:**
[What should happen once the issue is resolved, and how long it may take]
```

---

## Safe Actions (can do without asking)

These are low-risk clicks that don't change campaign structure or spend:
- Reading any page, billing screen, or delivery insight
- Clicking "See why" or "Learn more" on warning messages
- Clicking into rejected ads to read the rejection reason
- Clicking "Verify payment method" flow if prompted

## Ask Permission Before Doing

These change settings and require user confirmation first:
- Editing or removing account spending limit
- Adding/removing a payment method
- Editing ad set dates, budget, or targeting
- Unpausing or pausing any campaign element

## Never Do

- Delete any campaign, ad set, or ad
- Change creative (copy, image, video)
- Submit payment or enter card details on behalf of user
- Accept any terms or legal agreements

---

## Common Fixes Reference

| Issue | Fix |
|---|---|
| Account spending limit at €0 | Billing → Payment Settings → Remove spending limit |
| No backup card (prepaid only) | Ask user to add a debit/credit card as secondary |
| Ad in review >48hrs | User should contact Meta Support via Help Center |
| Audience too small (<1K) | Broaden targeting in Ad Set settings |
| End date already passed | Edit Ad Set → extend end date |
| Payment method needs verification | Follow the Confirm Card flow in Payment Settings |
| Currency mismatch | User needs to contact Meta Support — can't be self-fixed |
| Account restricted/disabled | User must appeal at facebook.com/help/contact/1426358510773349 |

---

## Communication Style

- Narrate what you're doing as you navigate: *"I'm opening the Billing tab now to check your payment settings..."*
- When you find something, explain it in plain language before using Meta's terminology
- Be specific: say *"Your account spending limit is set to €0, which blocks all ad delivery"* not just *"there's an issue"*
- If unsure what something means, say so — don't guess
- After fixing anything, confirm with the user before moving to the next step
