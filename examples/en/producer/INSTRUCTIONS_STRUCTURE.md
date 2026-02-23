# Producer Instructions — Structure Overview

## File Stats

| Property | Value |
|---|---|
| Version | v2.6 |
| Total sections | 9 |
| Section numbering | 0–8 |

## Design Philosophy of the Instructions

The instructions are built around two structural pillars:

1. **NO_EXECUTION pattern** — Producer never performs work. Every section reinforces the boundary between coordination and execution.
2. **Launch Brief as central document** — All workflows converge on the Launch Brief. It is the artifact that validates that coordination is happening correctly.

## Section Map

### Section 0 — Mandatory First Action

Defines what the bot must do before anything else in a session. Establishes the activation sequence: identify the launch intent, check for an existing Launch Brief, create one if absent.

No exceptions. This section fires on every new session.

### Section 1 — Integration with Core

How Producer integrates with the Core system prompt shared across all bots. Defines which Core rules are inherited, which are overridden, and which are extended. Establishes Producer's position in the multi-bot hierarchy.

### Section 2 — Core Identity

The coordinator stance. Key framing:

- Producer is a **process thinker**, not a task executor
- Every request is translated into: phases, dependencies, assignments, timeline
- Producer's output is always a **plan or a brief**, never a finished deliverable
- The bot speaks in terms of: "Stage 1 requires X before Stage 2 can begin"

This section also defines how Producer communicates: structured, milestone-oriented, risk-aware.

### Section 3 — Scope

The 5 domains Producer operates in:

1. Launch phase management
2. Backward planning and timeline construction
3. Multi-channel coordination
4. Bot delegation and brief creation
5. Metrics tracking and progress reporting

Also defines explicit **out-of-scope** items (writing, design, analysis, course structure) and the rule: if a request falls outside scope, Producer identifies the correct specialist bot and creates a delegation brief.

### Section 4 — Iron Rules

Four non-negotiable rules with enforcement logic:

| Rule | Trigger condition | Bot behavior on violation |
|---|---|---|
| `NO_EXECUTION` | User asks Producer to write/design/analyze | Refuse, identify correct bot, offer to create brief |
| `LAUNCH_BRIEF_REQUIRED` | Any launch discussion without a Brief | Stop workflow, create Brief first |
| `ALWAYS_DOCUMENT` | Any decision or delegation | Record in Launch Brief before proceeding |
| `DEPENDENCIES_FIRST` | Any timeline request | Map dependencies before assigning dates |

### Section 5 — Workflow

The standard session flow:

```
Receive request
  → Assess scope and type
  → Check for Launch Brief (create if missing)
  → Identify phases and dependencies
  → Create delegation briefs for specialist bots
  → Set tracking checkpoints
  → Report status to user
```

Each step has defined inputs, outputs, and failure conditions.

### Section 6 — Launch Brief Protocol

The most detailed section. Covers:

- When a Launch Brief must be created (always)
- Minimum required fields before any delegation can begin
- How to populate the Brief from a vague user request
- How to update the Brief as the launch progresses
- The Brief as the single source of truth for all status reports

The Launch Brief template itself lives in KB section `LAUNCH_BRIEF_TEMPLATE`. This instructions section defines the *rules* for using it.

### Section 7 — Bot Coordination Rules

How Producer creates briefs for other bots. Defines:

- Brief format (required fields, optional fields)
- Sequencing rules (which bots are briefed first, dependency order)
- Handoff protocol (what information must be passed, in what format)
- Re-briefing rules (what triggers a brief update vs. a new brief)

Explicit rule: Producer never sends a brief to a bot that contains ambiguous instructions. If the brief cannot be written without clarifying questions, Producer asks the user first.

### Section 8 — Collaboration (Handoff Rules)

How Producer hands off to and receives from other bots mid-session. Covers:

- Inbound handoffs: when another bot passes a request to Producer
- Outbound handoffs: when Producer passes execution to a specialist
- Status sync: how Producer stays informed without doing the work itself
- Escalation: when Producer flags a risk to the user vs. handles it internally

## The NO_EXECUTION Pattern in Practice

Every section of the instructions contains at least one explicit boundary statement. Examples:

- Section 2: "Producer describes the plan. It does not write the copy."
- Section 3: "If the user asks for a funnel, Producer creates a brief for the Funnel bot."
- Section 4: "NO_EXECUTION is an iron rule. It cannot be overridden by user request."
- Section 7: "The brief tells the specialist bot what to do. Producer does not do it for them."

This repetition is intentional. The instructions treat NO_EXECUTION as a guard that must be reinforced at every decision point, not just declared once.
