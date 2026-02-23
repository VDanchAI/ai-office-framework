# Producer KB — Structure Overview

## File Stats

| Property | Value |
|---|---|
| Version | v2.4 |
| Total lines | 3182 |
| Main sections | 31 |
| Subsections | 77 |
| Router version | v5.2 (flat) |

## Architecture: Main Sections + Contextual Subsections

The KB uses a **flat router architecture** (v5.2). Every section is a named block retrievable by exact key. Subsections are embedded within their parent section and addressed via dotted notation (e.g., `LAUNCH_PHASES.PRE_LAUNCH`).

This means:
- No nested files or folders — everything lives in one flat KB
- The router resolves section keys at query time, not at load time
- Subsections are contextual: they activate only when the parent section is retrieved and the query matches a subsection key

## Section Map

### Core Planning Sections

| # | Section Key | Description | Subsections |
|---|---|---|---|
| 1 | `AUTOMATION_OVERVIEW` | What can be automated in launches; n8n and Airtable patterns | 3 |
| 2 | `LAUNCH_PHASES` | Pre-launch / launch / post-launch structure and stage definitions | 6 |
| 3 | `BACKWARD_PLANNING` | Timeline planning from deadline, critical path, dependency mapping | 4 |
| 4 | `CHANNEL_MATRIX` | Multi-channel campaign coordination: which channels, sequencing, sync rules | 5 |
| 5 | `BOT_COORDINATION` | Delegation rules, brief creation protocols, handoff sequencing | 4 |
| 6 | `LAUNCH_BRIEF_TEMPLATE` | Master template for the central planning document | 7 |

### Operational Sections

| # | Section Key | Description | Subsections |
|---|---|---|---|
| 7 | `METRICS` | KPI definitions, tracking checkpoints, reporting formats | 4 |
| 8 | `COMMON_MISTAKES` | Risk identification patterns, failure modes, early warning signals | 5 |
| 9 | `COMMUNICATION_TEMPLATES` | Session communication protocols, status update formats | 3 |
| 10–31 | *(additional sections)* | Supporting reference material, checklists, edge case handling | 36 |

**Total subsections across all sections: 77**

## Flat Router Logic (v5.2)

```
query → router → section key match → retrieve section block
                                   → if subsection key present → retrieve subsection block
                                   → return to context window
```

Key properties of the flat router:

- **Single-level resolution**: The router does not recurse. It matches one key per query.
- **Subsection passthrough**: If a query contains both a section key and a subsection key, the router returns the subsection block, not the full section.
- **No ambiguity resolution**: If a query matches multiple keys, the router selects by priority rank (defined in the router config, not in the KB).
- **Stateless**: The router carries no session state. Each retrieval is independent.

## Subsection Naming Convention

Subsections follow the pattern: `PARENT_KEY.SUBSECTION_NAME`

Examples:
- `LAUNCH_PHASES.PRE_LAUNCH`
- `LAUNCH_PHASES.LAUNCH_DAY`
- `LAUNCH_PHASES.POST_LAUNCH`
- `BACKWARD_PLANNING.CRITICAL_PATH`
- `BOT_COORDINATION.BRIEF_FORMAT`
- `LAUNCH_BRIEF_TEMPLATE.RISK_REGISTER`

## Design Rationale

The flat architecture was chosen over hierarchical file structures because:

1. **Retrieval speed** — Single key lookup, no directory traversal
2. **Transparency** — The full section map is visible in one place
3. **Maintainability** — Adding a section does not change the router logic
4. **Predictability** — The bot always knows exactly what it retrieved and why
