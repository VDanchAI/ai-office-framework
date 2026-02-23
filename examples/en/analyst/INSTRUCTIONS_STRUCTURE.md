# Instructions Structure — Analyst Instructions v2.4

**Version:** 2.4
**Sections:** 9 (numbered 0–8)
**Core dependency:** Yes (loads shared AI Office Core on startup)

---

## Section map

| # | Title | Purpose |
|---|---|---|
| 0 | Mandatory First Action | Bootstraps the bot — loads Core before anything else |
| 1 | Integration with Core | Defines priority hierarchy between Core and Analyst-specific rules |
| 2 | Core Identity | Role definition, prime directive, My Card |
| 3 | Scope | What this bot handles + delegation table |
| 4 | Iron Rules | Hard constraints that cannot be overridden |
| 5 | Data Sources | Where data comes from, how to request it |
| 6 | Analysis Workflow | Step-by-step process from input to output |
| 7 | Output Formats | Insight card, report, dashboard brief structures |
| 8 | Collaboration | Handoff rules and routing to other bots |

---

## Section details

### Section 0 — Mandatory First Action
**Purpose:** Ensures the shared Core is loaded before the bot does anything.
**Key elements:**
- Explicit load instruction for Core file
- Blocks any response until Core is confirmed loaded
- Prevents the bot from running in a degraded state

---

### Section 1 — Integration with Core
**Purpose:** Establishes what happens when Analyst rules and Core rules conflict.
**Key elements:**
- Priority hierarchy (Core > Analyst-specific, with defined exceptions)
- List of Analyst overrides that take precedence over Core defaults
- Merge rules for overlapping behaviors

---

### Section 2 — Core Identity
**Purpose:** Defines who this bot is and how it introduces itself.
**Key elements:**
- Role name and one-line description
- Prime directive (verbatim): "Every insight must answer 'so what?'. Data without recommendation is a report, not analysis."
- Philosophy statement: translator from data language to decision language
- My Card — the self-introduction block shown on first interaction

---

### Section 3 — Scope
**Purpose:** Clear boundaries on what this bot handles and what it does not.
**Key elements:**
- Covered domains table (Social Media, Email, Funnel, Content ROI, Retention)
- Delegation table — maps out-of-scope requests to the correct bot
- Boundary cases (what to do when a request is partially in-scope)

---

### Section 4 — Iron Rules
**Purpose:** Hard constraints enforced on every output, no exceptions.
**Key elements:**
- No data dumps — raw numbers are never delivered without interpretation
- CIRI always — every analytical output follows Context → Insight → Recommendation → Impact
- Never invent numbers — if data is missing, the bot says so and requests it
- Actionable or nothing — if no recommendation is possible, the bot explains why
- Additional guardrails specific to the analytical role

---

### Section 5 — Data Sources
**Purpose:** Defines where data comes from and how the bot requests missing data.
**Key elements:**
- Accepted data source types (user-provided, platform exports, prior conversation)
- REQUEST format — standardized structure the bot uses when it needs data from the user
- Handling incomplete data sets
- What the bot does when data quality is insufficient for analysis

---

### Section 6 — Analysis Workflow
**Purpose:** Step-by-step process the bot follows from receiving a query to delivering output.
**Key elements:**
- Receive → Clarify → Gather Data → Analyze → Apply CIRI → Deliver
- Decision points at each stage (when to proceed, when to ask)
- How KB sections are selected during the Analyze step
- Quality check before delivery

---

### Section 7 — Output Formats
**Purpose:** Templates and structure for the three main output types.
**Key elements:**
- **Insight Card** — single-metric or single-question analysis (compact CIRI)
- **Report** — multi-metric structured analysis with sections
- **Dashboard Brief** — recommendations for dashboard layout and KPI selection
- Formatting rules (when to use tables, when to use bullets, length guidelines)

---

### Section 8 — Collaboration
**Purpose:** Rules for handing off to other bots in the AI Office.
**Key elements:**
- Handoff trigger conditions (when to route vs. when to stay)
- Handoff message format — what information to pass to the receiving bot
- Receiving handoff — how to process incoming context from other bots
- Loop prevention — rules to avoid bouncing requests between bots

---

## Design patterns

### CIRI enforcement
CIRI is enforced in two places: Section 4 (Iron Rules, as a hard constraint) and Section 7 (Output Formats, as a structural template). The duplication is intentional — Iron Rules say "always do CIRI," Output Formats show "here is what CIRI looks like."

### Data source protocol
The REQUEST format in Section 5 is a standardized block the bot uses consistently. This makes it easy for users to recognize when the bot needs data and what format to provide it in.

### Delegation network
Section 3 (Scope) and Section 8 (Collaboration) work together. Section 3 defines the boundaries; Section 8 defines what happens at those boundaries. The delegation table in Section 3 is mirrored by the handoff rules in Section 8.

### Section 0 as a safety mechanism
Loading Core as a mandatory first action (Section 0) is a structural pattern used across all AI Office bots. It ensures shared rules — including ethical constraints and office-wide protocols — are always active regardless of which bot-specific instructions follow.
