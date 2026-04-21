---
name: instagram-ads
description: >
  Create high-converting Instagram ad campaigns including ad copy, creative briefs, hooks,
  CTAs, targeting strategies, campaign structures, and full content calendars. Use this skill
  whenever the user mentions Instagram ads, Meta ads, sponsored posts, paid social, ad creative,
  ad copy, Instagram campaigns, boosted posts, story ads, reel ads, carousel ads, or anything
  related to advertising on Instagram — even if they just say "help me run ads" or "promote
  my product on Instagram." Also trigger for requests about audience targeting, ad budgets,
  A/B testing for social ads, or Meta Ads Manager strategy.
---

# Instagram Ads Skill

A skill for creating complete, conversion-focused Instagram ad campaigns — from strategy and
targeting through to final copy, creative briefs, and launch-ready assets.

---

## When You Receive a Request

Before writing anything, gather these inputs (check conversation first — many may already be
provided):

**Required**
- **Product / Service**: What is being advertised?
- **Goal**: Awareness, traffic, leads, sales, app installs, DMs?
- **Target audience**: Demographics, interests, behaviors, pain points
- **Budget** (if known): Daily or lifetime, total spend

**Nice to have**
- Brand voice / tone (fun, premium, authoritative, casual?)
- Existing creative assets (images, video, UGC)
- Competitor brands or reference ads they admire
- Landing page or destination URL

If the user hasn't provided enough to proceed, ask for the **Required** fields in a single
friendly message before writing any ads.

---

## Ad Format Selection Guide

Choose the right format based on the campaign goal:

| Format | Best For | Notes |
|---|---|---|
| **Single Image** | Awareness, simple offer, retargeting | Fast to produce, clear message |
| **Carousel** | Product range, step-by-step, before/after | 2–10 cards, each needs its own hook |
| **Reels / Video** | Cold audiences, storytelling, demos | Hook in first 1–2 seconds is critical |
| **Story** | Flash offers, urgency, retargeting | Vertical 9:16, 15 sec max for video |
| **Collection** | E-commerce product discovery | Requires catalog integration |

When the user doesn't specify a format, recommend 2–3 formats based on their goal and explain why.

---

## Core Copywriting Framework

Every Instagram ad needs these five elements:

### 1. Hook (first line / first 2 seconds)
The single most important element. Must stop the scroll. Types:
- **Problem agitation**: "Still paying too much for X?"
- **Bold claim**: "We 10x'd our sales in 30 days. Here's how."
- **Curiosity gap**: "Nobody talks about this side of [topic]."
- **Direct address**: "Attention [specific audience]:"
- **Surprising stat**: "67% of [audience] struggle with [problem]."

### 2. Body Copy
- Lead with the biggest benefit, not features
- Use short paragraphs (1–2 lines max)
- Include social proof if available (ratings, testimonials, user counts)
- Address the primary objection
- Match the energy of the hook

### 3. CTA (Call to Action)
Match the CTA to the campaign goal:
- **Sales**: "Shop now", "Grab yours", "Order today — [offer expires]"
- **Leads**: "Get your free [lead magnet]", "Book a call", "Download now"
- **Traffic**: "Read the full story", "See how it works", "Learn more"
- **DMs**: "DM us the word [keyword] to get started"

### 4. Visual Direction (Creative Brief)
For each ad variation, provide:
- **Scene**: What does the viewer see?
- **Mood/style**: Lifestyle, UGC-style, clean product, dramatic, etc.
- **Text overlay**: If any, what does it say and where?
- **Aspect ratio**: 1:1 (feed), 9:16 (story/reel), 4:5 (portrait feed)
- **Color/brand notes**: Palette, fonts, logo placement

### 5. Audience Targeting
See `references/targeting.md` for detailed targeting playbooks.

---

## Output Formats

### Single Ad Output
```
**FORMAT**: [Single Image / Carousel / Reel / Story]
**GOAL**: [Campaign objective]
**AUDIENCE**: [Who sees this]

---
PRIMARY TEXT:
[Full ad copy — hook + body + CTA]

HEADLINE: [Short punchy headline, 40 chars max]
DESCRIPTION: [Optional 1-line sub-headline for link ads]

CREATIVE BRIEF:
- Scene: [What to shoot/design]
- Style: [Aesthetic direction]
- Overlay text: [Any text on the visual]
- Aspect ratio: [1:1 / 4:5 / 9:16]
```

### Campaign Output (multiple ads)
When producing a full campaign, always deliver:
1. **Campaign overview** — goal, structure, budget allocation recommendation
2. **3–5 ad variations** — different hooks/angles targeting the same audience
3. **Audience targeting recommendations** — cold, warm, retargeting layers
4. **A/B test plan** — what to test first and why

---

## Campaign Structure Best Practices

### The 3-Layer Funnel
```
TOFU (Cold) — Awareness/Interest
  └─ Broad or interest-based targeting
  └─ Video or Reel format preferred
  └─ Problem/story angle copy

MOFU (Warm) — Consideration
  └─ Website visitors, video viewers, engagers (30–90 days)
  └─ Carousel or single image
  └─ Benefit-led copy, social proof

BOFU (Hot) — Conversion/Retargeting
  └─ Add-to-cart, past purchasers, email list
  └─ Single image or story
  └─ Urgency, offer, objection-handling copy
```

### Budget Guidance (when asked)
- **Testing phase**: $20–50/day minimum per ad set; kill ads with CPM > 3x benchmark after 3 days
- **Scaling**: Only scale winning creative — increase budget ≤ 20% every 48hrs
- **Split**: Roughly 60% TOFU / 25% MOFU / 15% BOFU for new campaigns

---

## Hooks Swipe File

Use these as starting templates, always customized to the brand:

**E-commerce**
- "This [product] sold out 3 times. We finally restocked."
- "Why does everyone keep buying [product]?"
- "I thought [price] was too expensive. Then I tried it."

**Service / B2B**
- "We helped [X clients] get [result] in [timeframe]."
- "Here's the exact system we use to [outcome]."
- "If you're a [job title] and you're not doing this, you're leaving money on the table."

**App / SaaS**
- "Delete [competitor]. You don't need it anymore."
- "The [category] app nobody's talking about."
- "[Problem]? There's an app for that now."

**Local Business**
- "Best [category] in [city]? We'll let [X] 5-star reviews speak for themselves."
- "If you live in [city] and haven't tried [X], you're missing out."

---

## Reference Files

Load these when needed:

- **`references/targeting.md`** — Detailed Meta audience targeting playbooks by niche
- **`references/compliance.md`** — Meta ad policy rules, restricted categories, copy limits

---

## Quality Checklist

Before presenting any ad output, verify:

- [ ] Hook is in the first line and creates immediate curiosity or relevance
- [ ] Primary text is under 125 characters before the "more" truncation (or deliberately longer for storytelling)
- [ ] CTA matches the campaign objective
- [ ] Creative brief gives a designer/photographer enough direction to execute without a call
- [ ] At least 3 copy variations provided (different hooks, same core offer)
- [ ] Targeting recommendation included
- [ ] No restricted language (see `references/compliance.md` for flagged terms)

---

## Example Interaction

**User**: "Write Instagram ads for my protein powder brand. We sell to gym-going women 25–35."

**Claude should produce**:
1. 3 ad variations (e.g., hook angles: taste, results, clean ingredients)
2. Recommended formats (e.g., Reel for cold, carousel for retargeting)
3. Targeting: Interest-based cold → engager retargeting → purchaser lookalike
4. Creative briefs for each ad
5. A/B test recommendation (e.g., test hook style first)
