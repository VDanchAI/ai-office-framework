# Marketer KB — Knowledge Base Structure

## Overview

| Attribute | Value |
|---|---|
| Version | v4.2 |
| Total lines | 26,681 |
| Sections | 29 |
| Router type | Flat (v5.6) |
| Notable | One of the largest KBs in the AI Office suite |

The KB is a single large document with a **flat router** — a lookup table at the top that
maps keywords and intent signals to section anchors. The model does not traverse the file
linearly; it pattern-matches the request against the router and jumps directly to the
relevant section(s). Multiple sections can be activated for a single request.

---

## Section Map (29 sections, grouped by theme)

### Paid Acquisition (4 sections)

| # | Section ID | Domain |
|---|---|---|
| 1 | `PAID_ADS` | Facebook Ads, Instagram Ads, Google Ads, Telegram Ads |
| 2 | `AUDIENCES` | Audience architecture, lookalikes, segmentation |
| 3 | `CREATIVES` | Creative strategy, hook frameworks, brief structure |
| 4 | `BIDDING` | Bid strategies, budget allocation, scaling playbooks |

### Email & CRM (3 sections)

| # | Section ID | Domain |
|---|---|---|
| 5 | `EMAIL_MARKETING` | Sequences, newsletters, automation, deliverability |
| 6 | `CRM_SYSTEMS` | CRM setup, pipeline stages, lead scoring |
| 7 | `SEGMENTATION` | List segmentation, behavioral triggers, tagging logic |

### Funnels & Conversion (4 sections)

| # | Section ID | Domain |
|---|---|---|
| 8 | `FUNNELS` | Funnel architecture, stage logic, conversion rates |
| 9 | `LANDING_PAGES` | LP structure, offer framing, CTA optimization |
| 10 | `UPSELLS` | Upsell/downsell/cross-sell mechanics |
| 11 | `CHECKOUT` | Cart abandonment, checkout optimization |

### Launches (2 sections)

| # | Section ID | Domain |
|---|---|---|
| 12 | `LAUNCHES` | Full launch strategy: pre-launch, launch, post-launch |
| 13 | `WEBINARS` | Webinar funnels, show-up rates, conversion tactics |

### Strategy & Positioning (4 sections)

| # | Section ID | Domain |
|---|---|---|
| 14 | `POSITIONING` | Market differentiation, messaging architecture |
| 15 | `COMPETITOR_ANALYSIS` | Competitive research, gap analysis, counter-positioning |
| 16 | `PRICING_PSYCHOLOGY` | Pricing tiers, anchoring, value framing |
| 17 | `OFFERS` | Offer construction, value stacks, guarantees |

### Economics & Analytics (4 sections)

| # | Section ID | Domain |
|---|---|---|
| 18 | `UNIT_ECONOMICS` | CAC, LTV, ROAS, break-even, payback period |
| 19 | `ANALYTICS` | GA4, Meta Pixel, UTM architecture, attribution |
| 20 | `AB_TESTING` | Test design, statistical significance, interpretation |
| 21 | `REPORTING` | Dashboard structure, KPI selection, reporting cadence |

### Retention & Growth (4 sections)

| # | Section ID | Domain |
|---|---|---|
| 22 | `RETENTION_LTV` | Retention tactics, churn analysis, LTV optimization |
| 23 | `REFERRAL` | Referral program design, mechanics, incentive structure |
| 24 | `REACTIVATION` | Win-back campaigns, dormant segment strategies |
| 25 | `LOYALTY` | Loyalty loops, community-as-retention |

### Non-Standard Tactics (4 sections)

| # | Section ID | Domain |
|---|---|---|
| 26 | `GUERRILLA` | Non-standard acquisition: PR stunts, virality, growth hacks |
| 27 | `REFRAMING` | Complete reframing research (~25,000 words) |
| 28 | `LINKEDIN` | LinkedIn marketing, B2B acquisition tactics |
| 29 | `YOUTUBE` | YouTube strategy, organic growth, ad integration |

---

## Flat Router — How It Works

```
[Request arrives]
       ↓
[Router scans for keywords + intent signals]
       ↓
[Matches 1–N section anchors]
       ↓
[Relevant sections loaded into context]
       ↓
[Response generated from matched content]
```

The router is defined as a structured lookup block at the top of the KB file. Each entry
contains: trigger keywords, intent patterns, and target section ID(s). A single request
for "launch Facebook campaign for course" would activate: `PAID_ADS`, `AUDIENCES`,
`FUNNELS`, and potentially `LAUNCHES` — all simultaneously.

---

## Notable Sections

**`REFRAMING`** (~25,000 words) is the largest single section — a complete domain on
cognitive reframing techniques applied to marketing, objection handling, and positioning.
It is the most referenced section in the KB for complex positioning tasks.

**`UNIT_ECONOMICS`** contains standardized calculation templates for CAC, LTV, ROAS,
break-even, and payback period. These are referenced in the Instructions to enforce
the "realistic numbers only" iron rule.

**`LAUNCHES`** contains a full launch playbook structure with phase-by-phase breakdowns,
typical conversion benchmarks by product type, and common failure patterns.

---

## Size Context

```
Total lines: 26,681
Equivalent to: ~200–220 pages of dense professional content
Largest KB in AI Office: Yes (Reframing section alone is ~25K words)
Update cadence: Version bumped when any section gets major revision
Current version: v4.2
```
