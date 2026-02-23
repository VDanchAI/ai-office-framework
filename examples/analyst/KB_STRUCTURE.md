# Knowledge Base Structure — Analyst KB v2.0

**Version:** 2.0
**Size:** 1318 lines
**Router type:** Flat (v5.2)
**Sections:** 8

---

## Router type note

A **flat router** is used when the KB has fewer than ~20 sections and queries map cleanly to one section at a time. The router reads the query, identifies a section ID, and loads only that section — keeping context window usage low.

For more complex KBs (20+ sections, overlapping domains, multi-step retrieval), a hierarchical or semantic router would be more appropriate. At 8 sections, flat routing is the right call here.

---

## Section table

| # | ID | Title | Purpose |
|---|---|---|---|
| 1 | `FORMULAS` | Core Metrics Formulas | Definitions and calculation formulas for all key metrics: conversion rate, CAC, LTV, churn, ROI, ROAS, email metrics |
| 2 | `BENCHMARKS` | Industry Benchmarks | Reference values by industry and channel for contextualizing client numbers |
| 3 | `ATTRIBUTION` | Attribution Models | Attribution model descriptions, UTM tracking conventions, multi-touch logic |
| 4 | `DASHBOARDS` | Dashboard Structure | Dashboard layout patterns, visualization choice by metric type, refresh cadence |
| 5 | `REPORTS` | Report Templates | Standard report formats for weekly/monthly/ad-hoc analysis |
| 6 | `FUNNELS` | Funnel Analysis | Funnel stage definitions, conversion benchmarks, drop-off diagnosis |
| 7 | `RED_FLAGS` | Warning Signs | Thresholds and patterns that signal problems requiring immediate attention |
| 8 | `QUICK_REFERENCE` | Quick Reference | Fast lookup for common one-question queries (e.g. "what is a good open rate?") |

---

## How the router is used

```
User query
    │
    ▼
Router v5.2 reads query
    │
    ├── keyword / intent match
    │
    ▼
Section ID selected (e.g. "BENCHMARKS")
    │
    ▼
Only that section is loaded into context
    │
    ▼
Analyst applies CIRI framework to produce output
```

---

## CIRI framework (applied at output stage)

The KB provides raw reference material. The Analyst always wraps KB content in the CIRI structure before delivering it to the user:

| Step | What it contains |
|---|---|
| **C** — Context | What was the situation / what data was provided |
| **I** — Insight | What the data actually means |
| **R** — Recommendation | What to do about it |
| **I** — Impact | What the expected result of that action is |

The KB does not enforce CIRI — the Instructions file does. The KB only stores factual reference content.

---

## Design notes

- Sections are self-contained: each can be loaded independently without requiring another section
- `QUICK_REFERENCE` intentionally duplicates some content from other sections for speed — this is by design
- `RED_FLAGS` is the only section with hard thresholds; all other sections use ranges and context-dependent values
- `FORMULAS` is the most frequently loaded section and is kept concise for this reason
