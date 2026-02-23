# Copywriter — Instructions Structure

> This document describes HOW the Copywriter's Project Instructions are organized.
> It shows instruction blocks, their purpose, and the logic behind them.
> The actual prompts and behavioral rules are not included.

## Overview

**Current version:** v6.1 | 8 sections | ~500 lines
**Purpose:** Define WHO the bot is, HOW it behaves, and WHAT rules it follows

---

## Section Map

### Section 0: MANDATORY FIRST ACTION
**Purpose:** Forces the bot to load Universal Core before doing anything.
**Why it's first:** Without Core, the bot ignores shared protocols (clarification, self-check, etc.)

```
Trigger: Session start
Action: Read UNIVERSAL_CORE → follow S1 Session Start → then respond
```

### Section 1: INTEGRATION WITH CORE
**Purpose:** Establishes where these instructions sit in the priority hierarchy.
**Key elements:**
- Priority stack (User Message > Core > Bot Instructions > Brandbook > KB > Judgment)
- List of Core protocols this bot must follow
- Error handling behavior

### Section 2: CORE IDENTITY
**Purpose:** Defines the bot's role, persona, and prime directive.
**Key elements:**
- **Role definition** — specific, not generic ("voice of the brand in text")
- **Who You ARE / Who You Are NOT** — prevents role drift
- **Prime directive** — one sentence, everything else serves this
- **Communication layers** — how the bot structures messages
- **My Card** — compact summary for cross-bot reference

**Design insight:** The "Who You Are NOT" table is critical. Without it, a creative bot starts doing analytics, a strategist starts writing copy. Clear boundaries = consistent behavior.

### Section 3: SCOPE
**Purpose:** Lists all task types this bot handles and explicitly excludes others.
**Key elements:**
- **My tasks:** Content types the bot creates (posts, articles, email copy, etc.)
- **Not my tasks:** What belongs to other bots + where to redirect

**Design insight:** Every "Not my task" points to a specific other bot. This creates natural handoff paths in a multi-bot office.

### Section 4: IRON RULES
**Purpose:** Non-negotiable, role-specific behavioral rules.
**Structure:** Numbered rules (4.1, 4.2, ...) each with: Rule + Why + Example

**Rules in this bot include:**
- Brandbook voice adherence
- KB consultation before writing
- No copy-paste from sources
- Clarification before starting
- Surgical edits over rewrites
- Handling knowledge gaps
- Anti-AI detection tactics (intentional imperfections)
- Structural diversity in content series
- Unpredictability markers

**Design insight:** The WHY behind each rule is crucial. A bot that understands reasoning handles edge cases better than one that just follows rules. "Don't use word X" is less effective than "Don't use word X because it's flagged by AI detectors — here's why."

### Section 5: WORKFLOW
**Purpose:** Step-by-step process for how the bot handles tasks.
**Key elements:**
- Standard task flow (receive → clarify → prepare → generate → check → deliver)
- Task-specific workflows (new post vs editing vs series creation)

### Section 6: OUTPUT FORMAT
**Purpose:** Defines what deliverables look like.
**Key elements:**
- Default structure and formatting
- Format variations by content type
- Length rules (never assume — always ask or follow brief)
- Tone/voice specifications

### Section 7: KB USAGE
**Purpose:** Role-specific rules for Knowledge Base interaction.
**Key elements:**
- Which sections to always consult for which task types
- When to combine multiple sections
- When KB lookup is optional (quick edits, small fixes)

### Section 8: COLLABORATION
**Purpose:** How this bot works with other bots in the AI Office.
**Key elements:**
- Handoff table: When user needs X → redirect to Bot Y → pass context Z
- REQUEST format for delegating to other bots
- What context to include in handoffs

---

## Design Patterns Used

### Pattern: Numbered Iron Rules
Rules are numbered (4.1, 4.2, ...) so they can be referenced in conversation:
- Bot: "Per rule 4.3, I should not copy-paste from the source."
- User: "Ignore rule 4.7 for this text." → Bot can selectively override.

### Pattern: "Who You Are NOT" Boundary
Explicit negation prevents the most common AI failure mode — trying to do everything.
Each "NOT" maps to another bot, creating a delegation network.

### Pattern: Mandatory First Action
Section 0 runs before anything else. Without this, bots often skip Core loading
and behave inconsistently (different response styles, missing clarification, etc.)

### Pattern: Workflow as Protocol
Instead of describing behavior ("the bot should..."), instructions define protocols
("Step 1 → Step 2 → Step 3"). Protocols are more reliably followed than descriptions.

---

## Evolution Notes

This file went through 6 major versions:
- **v1–v2:** Basic role definition, minimal rules
- **v3:** Added Iron Rules, scope boundaries
- **v4:** Added KB integration rules, workflow protocols
- **v5:** Added anti-AI detection rules, unpredictability markers
- **v6:** Added Core integration, collaboration section, refined identity

**Key lesson:** Instructions grow with the KB. As you add more knowledge, you need more rules for how to use it.
