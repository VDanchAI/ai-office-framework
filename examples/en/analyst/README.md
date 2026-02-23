# Data Insights & Performance Analyst

**Role type:** Analytical
**Maturity:** Production
**Stack:** Instructions v2.4 · KB v2.0 · Router v5.2

---

## What this bot does

Translates raw metrics into decisions. The Analyst does not deliver data dumps — it delivers CIRI packages: Context, Insight, Recommendation, Impact. Every output answers the question "so what?".

**Prime directive:** "Every insight must answer 'so what?'. Data without recommendation is a report, not analysis."

---

## Core expertise

| Domain | What is analyzed |
|---|---|
| Social Media | Reach, engagement, CTR, growth rate, content performance |
| Email Marketing | Open rate, CTR, CTOR, unsubscribe rate, deliverability |
| Sales Funnel | Conversion by stage, drop-off points, CAC, CPL |
| Content ROI | Cost per lead from content, payback period, attribution |
| Customer Retention | Churn rate, LTV, retention cohorts, reactivation |

---

## Key differentiators

- **CIRI framework** — every analysis follows Context → Insight → Recommendation → Impact
- **Benchmarks built-in** — numbers are compared to industry standards, not presented in a vacuum
- **Actionable only** — if there is no recommendation, there is no output
- **Delegation protocol** — knows exactly when to hand off to Copywriter, Marketer, Methodologist, or Tech Specialist

---

## Architecture

```
┌─────────────────────────────────────────┐
│              INSTRUCTIONS v2.4          │
│   (identity · scope · iron rules ·      │
│    workflow · output formats)           │
└────────────────┬────────────────────────┘
                 │ loads on start
                 ▼
┌─────────────────────────────────────────┐
│                  CORE                   │
│        (shared AI Office base)          │
└────────────────┬────────────────────────┘
                 │ routes queries to
                 ▼
┌─────────────────────────────────────────┐
│              KB v2.0                    │
│   Flat Router v5.2 · 8 sections         │
│   1318 lines                            │
│                                         │
│  FORMULAS · BENCHMARKS · ATTRIBUTION   │
│  DASHBOARDS · REPORTS · FUNNELS        │
│  RED_FLAGS · QUICK_REFERENCE           │
└─────────────────────────────────────────┘
```

---

## What is NOT this bot's job

| Request | Correct bot |
|---|---|
| Write a post or email | Copywriter |
| Fix a broken funnel | Marketer |
| Redesign course structure | Methodologist |
| Long-term strategic planning | Visionary |
| Set up analytics platform | Tech Specialist |

The Analyst flags these cases and routes them — it does not attempt to handle them.

---

## File inventory

| File | Purpose |
|---|---|
| `README.md` | This file — role overview |
| `KB_STRUCTURE.md` | Knowledge base organization |
| `INSTRUCTIONS_STRUCTURE.md` | Instructions file breakdown |
| `ROUTER_DEMO.json` | Example flat router (simplified) |
