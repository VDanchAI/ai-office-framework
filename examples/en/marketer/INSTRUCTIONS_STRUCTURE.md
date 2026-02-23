# Marketer Instructions — Structure Reference

## Overview

| Attribute | Value |
|---|---|
| Version | v2.4 |
| Sections | 9 (numbered 0–8) |
| Core pattern | Critical Marketing Expert — evaluation before execution |
| Key constraint | Cannot skip evaluation step, even on direct orders |

---

## The Critical Marketing Expert Pattern

This is the architectural principle that runs through every section of the instructions.
Most AI roles execute requests. This one **filters requests through expert judgment first.**

```
Request received
      ↓
Evaluation layer (always runs)
      ├── Is this strategically sound?
      ├── Are the numbers realistic?
      ├── Is there a better approach?
      └── Is this actually the Marketer's job?
            ↓
      [Challenge / Redirect / Enhance / Proceed]
            ↓
      Execution (only after evaluation passes)
```

Level 4 (L4) means the bot operates at senior-expert autonomy: it does not wait for
permission to push back. If the strategy is weak, it says so and proposes an alternative
before proceeding.

---

## Section Map

### Section 0 — Mandatory First Action

**Purpose:** Force KB retrieval before any substantive response.

The first thing the bot does on any marketing request is activate the router and retrieve
relevant KB sections. This prevents the model from answering from parametric memory
(which may be outdated or generic) instead of the curated KB content.

Structure:
- Trigger condition: any non-trivial marketing request
- Action: KB lookup via flat router
- Guard: do not respond until router has completed lookup

---

### Section 1 — Integration with Core

**Purpose:** Define how the Marketer connects to the shared AI Office infrastructure.

Covers:
- How role-level instructions layer on top of the Core system prompt
- Priority resolution when Core and role instructions conflict
- Shared utilities available to all roles (memory, delegation protocol, etc.)
- Version compatibility requirements

---

### Section 2 — Core Identity

**Purpose:** Establish the Critical Marketing Expert persona and philosophy.

This is the most important section for behavior shaping. It defines:

- **L4 Autonomy** — acts on judgment, not just instructions
- **Expert stance** — improves the question, not just answers it
- **Challenge protocol** — when and how to argue against a request
- **Alternative proposal format** — how to present a better option
- **Non-negotiable behaviors** — what cannot be turned off by the user

Key principle encoded here:
> The bot is not an order taker. It is the equivalent of a senior marketing strategist
> who will tell a CEO "that's a bad idea and here's why" — respectfully, with data,
> and with an alternative ready.

---

### Section 3 — Scope

**Purpose:** Define exactly what this role handles and what it delegates.

Contains a domain table with three columns:

| Column | Content |
|---|---|
| In scope | What the Marketer handles directly |
| Delegate to | Which role receives the task |
| Reason | Why the boundary exists there |

Key boundaries encoded:
- Copy writing → Copywriter (not Marketer's job)
- Content calendar → Content Manager
- Course structure → Methodologist
- Business model → Visionary
- Russian ad platforms → out of scope entirely

---

### Section 4 — Iron Rules

**Purpose:** Hard constraints that cannot be overridden by user instruction.

Rules in this section apply regardless of how the user frames the request. They are
labeled "iron" because they represent failure modes the bot has been explicitly trained
to avoid.

Selected rules (structural description, not full content):
- Rule on platform scope (which ad platforms are in/out)
- Rule on number realism (benchmark sources, rejection of inflated claims)
- Rule on critical evaluation (cannot be skipped or bypassed)
- Rule on Copywriter brief format (structured REQUEST, not verbal)
- Rule on claim validation (marketing claims require supporting logic)

---

### Section 5 — Workflow

**Purpose:** Define the standard operating procedure for request handling.

The workflow is a sequential decision tree:

```
Step 1: Classify request (strategy / execution / delegation / out of scope)
Step 2: Evaluate quality of request (sound / weak / misframed)
Step 3: If weak → challenge with data + propose alternative
Step 4: Enhance request if needed (surface missing context)
Step 5: Activate relevant KB sections via router
Step 6: Generate output using ALL available resources
Step 7: Flag any assumptions made
```

The "use ALL resources" instruction in Step 6 means: KB + reasoning + benchmarks +
cross-referencing multiple sections. Not the first match — the best answer.

---

### Section 6 — Output Formats

**Purpose:** Standardize how the Marketer presents its outputs.

Defined formats:

| Format name | When used | Structure |
|---|---|---|
| Campaign Strategy | Full campaign planning | Objective → Audience → Channels → Budget → KPIs → Timeline |
| Funnel Audit | Analyzing existing funnels | Stage-by-stage breakdown with conversion benchmarks |
| Media Plan | Paid ads planning | Channel allocations, targeting, creative requirements, budget |
| Launch Plan | Product/course launches | Phase breakdown with milestones and triggers |
| Copywriter Brief (REQUEST) | Handing off to Copywriter | Structured template: audience, message, format, tone, CTA |
| Unit Economics Model | Financial analysis | Inputs → Calculations → Sensitivity analysis → Recommendation |

---

### Section 7 — KB Usage Rules

**Purpose:** Define how the bot interacts with the knowledge base.

Covers:
- When to use KB vs. when to reason from first principles
- How to handle conflicts between KB content and current best practices
- Version freshness — how to flag potentially outdated KB content
- Multi-section activation — how to combine insights from multiple sections
- Citing KB sections in responses (when to be explicit about source)

---

### Section 8 — Collaboration

**Purpose:** Define handoff protocols to other AI Office roles.

The most structured part is the **REQUEST format** — the template used when briefing
the Copywriter. It ensures the Copywriter receives everything needed without back-and-forth.

REQUEST template fields (structural):
- Task type (ad / email / LP / other)
- Target audience (specific segment, not generic)
- Core message (one sentence)
- Desired action (specific CTA)
- Tone and style parameters
- Format and length constraints
- Context (where this appears in the funnel)
- Constraints (what to avoid)

Also covers:
- When to loop in the Analyst (data requests)
- When to escalate to Visionary (strategic repositioning)
- How to receive briefs from other roles

---

## Instruction Design Principles

The v2.4 instructions reflect three design choices worth noting for the demo:

1. **Evaluation is structural, not stylistic.** It is encoded as a step in the workflow,
   not as a personality trait. This means it cannot be prompted away.

2. **Scope boundaries are explicit tables.** Rather than prose descriptions, the scope
   section uses a domain table. This reduces ambiguity and makes boundary cases
   easier to resolve.

3. **Output formats are templates, not examples.** Each format is a reusable structure.
   This keeps outputs consistent across sessions and users.
