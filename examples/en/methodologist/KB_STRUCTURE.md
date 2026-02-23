# KB Structure — Methodologist

**Version:** v3.7
**Size:** 4958 lines
**Sections:** 10
**Router:** Flat (v5.2) — single-level dispatch, no nested routing

---

## Architecture Overview

```
KB v3.7
├── Router (flat, v5.2)          ← entry point for all queries
│
├── 01  RESULT_TYPES
├── 02  PSYCHOTECHNICAL_MYTH
├── 03  FORMAT_STRUCTURES
├── 04  TEMPLATES
├── 05  GROUP_WORK
├── 06  CHECKLISTS
├── 07  HANDOFFS
├── 08  ANTIPATTERNS
├── 09  THERAPY_GROUPS            ← expanded: 9 subsections
└── 10  BUSINESS_MODELS
```

The router receives a task description and returns the section identifier(s) to activate. No intermediary classification step — direct lookup.

---

## Router: Flat v5.2

Single dispatch layer. Input → section tag. Examples:

| Incoming task | Section activated |
|---|---|
| "Design a 2-hour workshop" | FORMAT_STRUCTURES, TEMPLATES |
| "What type of result is this outcome?" | RESULT_TYPES |
| "Create an exercise with motivation" | PSYCHOTECHNICAL_MYTH |
| "Check if the program is ready" | CHECKLISTS |
| "Group is stuck, no energy" | GROUP_WORK |
| "Pass this to the copywriter" | HANDOFFS |
| "This program has no clear outcome" | ANTIPATTERNS |
| "Set up an online therapy group" | THERAPY_GROUPS |
| "Price a cohort course" | BUSINESS_MODELS |

Flat architecture means: if a task touches two sections, both are activated in parallel — no priority queue, no sequential resolution.

---

## Sections

### 01 RESULT_TYPES
Classification framework for learning outcomes. Three types: Concept, Instrument, Resource. Each type has a different design logic, different exercise formats, and different success criteria. The Methodologist types every stated outcome before any design begins.

### 02 PSYCHOTECHNICAL_MYTH
Methodology for creating motivational entry context for assignments. Every exercise has a "myth" — a narrative or situational frame that makes the learning task feel necessary before the participant engages with the content. Contains: myth templates by result type, failure patterns, debrief connection rules.

**This section has no equivalent in standard instructional design frameworks. It is a proprietary concept specific to this KB.**

### 03 FORMAT_STRUCTURES
Structural templates for four main formats:
- Webinar
- Masterclass
- CBC (content-based course)
- Cohort course

Each template includes: duration brackets, engagement checkpoints, result-type compatibility, 2026 audience engagement tactics.

### 04 TEMPLATES
Formatting templates for program deliverables: program outlines, unit descriptions, exercise cards, session plans. Templates enforce the result-first structure — every template starts with an outcome field that must be filled before content fields unlock.

### 05 GROUP_WORK
Managing group dynamics in live program delivery. Covers: energy management, handling resistance, silence and disengagement, conflict protocols, pacing adjustments. Used when designing facilitated programs and when advising on delivery.

### 06 CHECKLISTS
Quality control instruments. Contains readiness checklists for: program design (pre-launch), single session (pre-delivery), exercise set (pre-use), handoff package (pre-delegation). Each checklist item maps to a specific failure mode documented in ANTIPATTERNS.

### 07 HANDOFFS
Delegation rules and brief formats for passing work to other roles: Copywriter, Marketer, Producer, Analyst. Each handoff template specifies what the Methodologist provides and what the receiving role needs to start without clarifying questions.

### 08 ANTIPATTERNS
Documented failure modes in educational program design. Organized by phase: design phase antipatterns, delivery phase antipatterns, business model antipatterns. Each entry: description of the pattern, why it fails, correction algorithm.

**Most common antipattern:** Content-first design — starting with "what I know" rather than "what participants will be able to do."

### 09 THERAPY_GROUPS
The largest expanded section. Full methodology for therapy group work. Nine subsections:

```
09  THERAPY_GROUPS
├── 09.1  Group Types          — classification: support, process, skills, psychoeducation
├── 09.2  Development Stages   — forming through termination, facilitator role per stage
├── 09.3  Selection            — intake criteria, contraindications, group composition
├── 09.4  Cohesion             — mechanisms, measurement, facilitation techniques
├── 09.5  Leadership           — co-facilitation models, authority dynamics
├── 09.6  Ethics               — confidentiality, dual relationships, boundary management
├── 09.7  Session Structure    — opening / working phase / closing, time allocation
├── 09.8  Online / Hybrid      — platform-specific adaptations, presence simulation
└── 09.9  Crisis Protocols     — member in crisis, group disruption, emergency referral
```

Scope note: therapy group design is the most methodologically dense area in the KB. The nine subsections reflect genuine complexity — each subsection has its own logic and cannot be collapsed into a general "group work" category.

### 10 BUSINESS_MODELS
Commercial design of educational products. Covers: pricing models (per-seat, subscription, cohort, hybrid), marketing metrics (CAC by channel), platform selection logic, financial metrics (LTV, break-even, payback period). Used when the Methodologist is consulted on product viability alongside program design.

---

## Design Principles Behind the KB

**Flat over nested.** The v5.2 router is deliberately non-hierarchical. Earlier versions (v4.x) used a two-level classification tree that introduced routing errors when tasks were ambiguous. Flat lookup with parallel section activation is more robust.

**Antipatterns as first-class citizens.** ANTIPATTERNS is a full section, not a footnote. Knowing what not to do is as operationally important as knowing what to do.

**Therapy groups as separate section.** Earlier versions folded therapy groups into GROUP_WORK. The v3.x KB separates them because the methodology is distinct enough — different ethics, different session logic, different selection criteria — that merged treatment produced errors.
