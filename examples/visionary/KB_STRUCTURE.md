# Visionary — Knowledge Base Structure

**KB version:** v5.0
**Router version:** v5.2 (hierarchical)
**Total sections:** 32
**Total domains:** 6

---

## Overview

This is the broadest knowledge base in the AI Office system. No other role covers this range — from raw cognitive mechanisms (D1) through strategic frameworks (D2), innovation methods (D3), organizational dynamics (D4), influence and meaning (D5), to AI governance (D6).

The KB uses a **hierarchical router** (v5.2): the router first identifies the domain, then routes to the section within that domain. This avoids flat-search performance degradation as KB size grows.

---

## Domain map

| Domain | Name | Sections | Priority | Coverage |
|---|---|---|---|---|
| D1 | THINKING_CORE | 5 | 10 | First principles, Bayesian thinking, decision making, cognitive biases, reasoning frameworks |
| D2 | STRATEGY_EXECUTION | 7 | 9 | Strategic frameworks, prioritization, goals, growth, scenario planning |
| D3 | INNOVATION | 4 | 7 | Lean Startup, MVP, creativity techniques, Design Thinking |
| D4 | ORGANIZATIONAL | 6 | 7 | Coaching, systems thinking, communication, feedback, negotiation |
| D5 | INFLUENCE_MEANING | 4 | 6 | Influence, persuasion, meaning/purpose, Ikigai, Stoicism |
| D6 | AI_GOVERNANCE | 1 | 8 | AI strategy, agents, build vs buy, governance |

**Total: 32 sections across 6 domains**

---

## Domain detail

### D1 — THINKING_CORE (priority 10, 5 sections)
The foundation. Highest priority — these sections inform HOW Visionary thinks, not just what it knows.

- First principles decomposition
- Bayesian updating and probability calibration
- Decision-making under uncertainty
- Cognitive biases catalog (recognition + countermeasures)
- Reasoning frameworks (inductive, deductive, abductive, analogical)

### D2 — STRATEGY_EXECUTION (priority 9, 7 sections)
The core toolkit for strategic work.

- Strategic frameworks: SWOT (with teeth), Porter's Five Forces, Blue Ocean, Business Model Canvas, JTBD
- Prioritization: RICE, MoSCoW, Kano model
- Goals: OKR methodology, Balanced Scorecard
- Growth: acquisition, retention, expansion mechanics
- Competitive dynamics
- Resource allocation
- Scenario planning and stress-testing

### D3 — INNOVATION (priority 7, 4 sections)

- Lean Startup methodology
- MVP design and validation
- Creativity techniques (SCAMPER, lateral thinking, analogical reasoning)
- Design Thinking (empathy → define → ideate → prototype → test)

### D4 — ORGANIZATIONAL (priority 7, 6 sections)

- Coaching frameworks (GROW, situational leadership)
- Systems thinking (feedback loops, archetypes, leverage points)
- Communication architecture
- Feedback design (giving, receiving, cadence)
- Negotiation (principled negotiation, BATNA, anchoring)
- Organizational change dynamics

### D5 — INFLUENCE_MEANING (priority 6, 4 sections)

- Influence and persuasion principles (Cialdini, narrative, framing)
- Stakeholder mapping and alignment
- Meaning and purpose frameworks
- Ikigai and Stoicism as strategic orientation tools

### D6 — AI_GOVERNANCE (priority 8, 1 section)
Single section, high priority — reflects current strategic importance.

- AI strategy for organizations
- Agent frameworks and orchestration patterns
- Build vs buy vs integrate decision criteria
- Governance, risk, and accountability

---

## Router logic (v5.2)

```
Input query
    └─ Domain classifier (6 candidates)
          ├─ D1 match → section router (5 candidates)
          ├─ D2 match → section router (7 candidates)
          ├─ D3 match → section router (4 candidates)
          ├─ D4 match → section router (6 candidates)
          ├─ D5 match → section router (4 candidates)
          └─ D6 match → section router (1 candidate)
```

Priority weights influence domain selection when query spans multiple domains. D1 (priority 10) is checked first for any query involving reasoning or decision-making. D6 (priority 8) is checked ahead of D3/D4/D5 for AI-related queries.

---

## Notes

- KB v5.0 added D6 (AI_GOVERNANCE) — previously absent
- Router v5.2 introduced priority weighting at domain level (previously flat)
- 32 sections is the current ceiling before performance review is triggered
- Cross-domain integration sections (5) handle queries that genuinely span domains (e.g., "AI strategy for a team resisting change" = D6 + D4)
