# Document Hierarchy

This document explains how documents are structured, loaded, and interact in the AI Office framework. Read [architecture.md](./architecture.md) first for a system-level overview.

---

## 1. The Four Document Types

Every bot in the system uses a combination of up to four document types. Each type has a distinct role and scope.

---

### Universal Core

**File pattern:** `UNIVERSAL_CORE_v[X]_[Y].md`
**Template:** `templates/TEMPLATE_CORE.md`

The Universal Core is the shared protocol loaded into every Claude Project, for every bot, without exception. It defines how bots think and communicate — not what they know or who they are.

**What it contains:**

| Section | Purpose |
|---|---|
| Loading Order | Sequence in which documents are loaded at session start |
| Session Start | Required actions when a new conversation begins |
| KB Navigation | How to use the Router to locate and read KB sections |
| Core Protocols | Clarify, Think, Expert Mode, Self-Check, Context Tracking |
| Communication Rules | Tone, format, response structure |
| Technical Operations | File handling, code output, tool use |
| Quality Protocol (D.A.O.S.) | Core quality assurance cycle |

**Versioning:** One file, maintained centrally. All bots use the same version. When the Core is updated, all bots inherit the update automatically — no per-bot changes needed.

---

### Knowledge Base (KB)

**File pattern:** `[Role]_Knowledge_Base_v[X]_[Y].md`
**Template:** `templates/TEMPLATE_KB.md`

The KB contains domain expertise for a specific role. Each bot has one main KB. Project-specific KBs can be added when a bot needs context that is scoped to a particular client or engagement.

**Internal structure:**

```
[Role]_Knowledge_Base_v[X]_[Y].md
│
├── Router (JSON block at the top of the file)
│   └── Index of all sections with triggers and anchors
│
└── Sections (markdown content below the Router)
    ├── #S1_TOPIC_NAME
    ├── #S2_TOPIC_NAME
    └── ...
```

The Router is always at the top. Sections follow below it, each identified by a unique anchor in the format `#S[number]_[TOPIC_NAME]`.

**Size range across the system:**

| Bot | KB Size |
|---|---|
| Analyst | ~1,300 lines |
| Copywriter | ~4,500 lines |
| Marketer | ~27,000 lines |

KBs this large cannot be read in full at query time. The Router exists precisely to avoid that — only the matching section is ever loaded.

**Router types** — see Section 4 for full details.

---

### Project Instructions

**File pattern:** `[Role]_Project_Instructions_v[X]_[Y].md`
**Template:** `templates/TEMPLATE_INSTRUCTIONS.md`

Project Instructions define who the bot is, what it does, and how it behaves. This is the role definition document, loaded as the "custom instructions" field in a Claude Project.

**Standard sections:**

| Section | What it defines |
|---|---|
| Mandatory First Action | What the bot does before anything else in a session |
| Core Integration | How to locate and load the Universal Core and KB |
| Identity | Role name, persona, voice |
| Scope | What this bot handles vs. what it refers elsewhere |
| Iron Rules | Absolute constraints that cannot be overridden |
| Workflow | Step-by-step process for the bot's primary tasks |
| Output Formats | How responses are structured and formatted |
| KB Usage | When and how to consult the KB |
| Collaboration | How this bot interacts with other bots in the system |

Each bot's Project Instructions are unique. Two bots may share a Universal Core but will always have distinct Project Instructions.

---

### Add-ons

**File pattern:** `[Addon_Name]_v[X]_[Y].md`
**Template:** `templates/TEMPLATE_ADDON.md`

Add-ons extend a bot's expertise in a specific area without modifying its core KB. They are optional, loaded on demand, and can be shared across multiple bots.

**Characteristics:**
- Each add-on has its own mini-Router and sections (same structure as a KB, smaller scale)
- Not permanently loaded — only brought in when the task requires them
- Can belong to one bot or be shared across several (e.g., a Brandbook Voice module used by both Copywriter and Marketer)

**Examples of add-ons in use:**

| Add-on | Used by |
|---|---|
| Social Media Specs | Copywriter, SMM Manager |
| Brandbook Voice | Copywriter, Marketer, PR Bot |
| Platform Restrictions | Marketer, Ad Manager |

---

## 2. Loading Order

Documents are loaded in a fixed sequence at the start of every session. This order is defined in the Universal Core and must never be changed.

```
Session Start
│
├── Step 1: Universal Core          ← always first, no exceptions
│
├── Step 2: Project Instructions    ← role identity and behavior rules
│
├── Step 3: KB Router ONLY          ← the index, not the content
│
├── Step 4: KB Section              ← only the section matching the query
│           (loaded per query, not upfront)
│
└── Step 5: Add-ons                 ← only if the task requires them
            (loaded per task, not permanently)
```

**KEY RULE: Never load the entire KB.**

The KB Router is loaded once at session start. When a query arrives, the bot matches it against the Router's triggers, identifies the relevant section anchor, and reads only that section. The rest of the KB is never loaded into context.

This is not a suggestion — it is a hard constraint enforced by the Universal Core. Loading the full KB on large files (e.g., 27,000 lines) would exhaust context and degrade performance.

---

## 3. Priority Hierarchy

When documents conflict — for example, if Project Instructions say one thing and the Universal Core says another — priority determines which wins. Higher number = higher priority.

| Priority | Document / Rule Type | Example |
|---|---|---|
| 0 | Default Claude behavior | General assistant defaults |
| 1 | Add-ons | Platform-specific formatting rules |
| 2 | KB content | Domain knowledge, factual content |
| 3 | Project Instructions | Role scope, output format, persona |
| 4 | Universal Core | Core protocols, D.A.O.S., session rules |
| 5 | Iron Rules | Hard limits that cannot be overridden by anything |

**Conflict resolution:** When two documents contradict each other, the one with the higher priority number wins. No exceptions.

Iron Rules (Priority 5) exist in Project Instructions as explicit constraints. They override everything, including the Universal Core. Example: "Never generate content in language X" is an Iron Rule — it beats any general-purpose instruction from the Core.

---

## 4. Router Deep Dive

The Router is a JSON block at the top of every KB file. It is the navigation index. The bot reads the Router first, finds the right section, then reads only that section.

There are two Router types depending on KB size.

---

### Flat Router

Used when the KB has fewer than 20 sections.

**Structure:**

```json
{
  "router_version": "1.0",
  "router_type": "flat",
  "sections": [
    {
      "id": "S1",
      "title": "Audience Research Methods",
      "anchor": "#S1_AUDIENCE_RESEARCH",
      "triggers": ["audience", "research", "target", "segment", "persona"],
      "description": "Frameworks for defining and analyzing target audiences",
      "priority": "high"
    },
    {
      "id": "S2",
      "title": "Content Strategy",
      "anchor": "#S2_CONTENT_STRATEGY",
      "triggers": ["content", "strategy", "editorial", "calendar", "planning"],
      "description": "Content planning and editorial strategy frameworks",
      "priority": "medium"
    }
  ]
}
```

**Lookup flow:**

```
Query received
     │
     ▼
Match query terms against triggers in each section entry
     │
     ▼
Identify best match → get anchor value
     │
     ▼
Jump to that anchor in the KB body
     │
     ▼
Read section content
```

Each section entry contains:
- `id` — short identifier (S1, S2, ...)
- `title` — human-readable name
- `anchor` — the markdown anchor to jump to (`#S1_AUDIENCE_RESEARCH`)
- `triggers` — keywords that cause this section to be selected
- `description` — one-line summary of what the section covers
- `priority` — used when multiple sections match (higher priority section wins)

---

### Hierarchical Router

Used when the KB has 20 or more sections. A single flat list becomes unwieldy at that scale — matching degrades and the Router itself becomes large enough to slow context loading.

The Hierarchical Router introduces two levels: a Master Router at the domain level, and Sub-Routers at the section level.

**Structure:**

```
Master Router (domain level)
├── Domain: Audience & Research
│   └── Sub-Router → sections S1–S6
├── Domain: Content Strategy
│   └── Sub-Router → sections S7–S14
├── Domain: Campaign Management
│   └── Sub-Router → sections S15–S22
└── Domain: Analytics & Reporting
    └── Sub-Router → sections S23–S28
```

**Two-stage lookup:**

```
Query received
     │
     ▼
Stage 1: Match against Master Router domain triggers
     │
     ▼
Identify domain → load that domain's Sub-Router
     │
     ▼
Stage 2: Match against Sub-Router section triggers
     │
     ▼
Identify section → get anchor
     │
     ▼
Jump to anchor → read section
```

**Master Router entry (example):**

```json
{
  "id": "D3",
  "domain": "Campaign Management",
  "sub_router_anchor": "#SUBROUTER_CAMPAIGNS",
  "triggers": ["campaign", "launch", "budget", "ad", "promotion", "funnel"],
  "section_count": 8
}
```

**Sub-Router entry (example):**

```json
{
  "id": "S17",
  "title": "Budget Allocation Models",
  "anchor": "#S17_BUDGET_ALLOCATION",
  "triggers": ["budget", "allocate", "spend", "distribution", "CPL", "ROAS"],
  "description": "Models for distributing campaign budget across channels"
}
```

The Sub-Router itself is stored as a section within the KB body (at its own anchor), not as a separate file. This keeps the KB self-contained.

---

## 5. Versioning

All files use a two-part version number in the filename.

**Format:** `v[MAJOR]_[MINOR]`

| Version part | When it increments | Example change |
|---|---|---|
| MAJOR | Structural changes | New sections added, sections removed, Router reorganized |
| MINOR | Content changes | Edits within existing sections, new examples, corrections |

**Examples:**
- `Marketer_Knowledge_Base_v3_0.md` → `v3_1.md` after adding examples to an existing section
- `Marketer_Knowledge_Base_v3_1.md` → `v4_0.md` after adding three new sections and reorganizing the Router

**Bot behavior:** When multiple versions of a file exist, the bot selects the highest version automatically. No manual version pinning is needed.

**Router version:** The Router tracks its own version inside the JSON block (`"router_version": "1.2"`), independently from the KB file version. The Router version increments when the Router structure changes — new sections added to the index, trigger lists updated, domain groupings changed — even if no KB body content changed.

---

## 6. File Naming Convention

All files follow a consistent naming pattern. No spaces — use underscores.

```
Universal Core:
  UNIVERSAL_CORE_v[X]_[Y].md
  Example: UNIVERSAL_CORE_v2_1.md

Knowledge Base:
  [Role]_Knowledge_Base_v[X]_[Y].md
  Example: Marketer_Knowledge_Base_v4_2.md
  Example: Analyst_Knowledge_Base_v1_3.md

Project Instructions:
  [Role]_Project_Instructions_v[X]_[Y].md
  Example: Copywriter_Project_Instructions_v2_0.md

Add-ons:
  [Addon_Name]_v[X]_[Y].md
  Example: Brandbook_Voice_v1_2.md
  Example: Social_Media_Specs_v3_0.md
  Example: Platform_Restrictions_v1_1.md
```

**Role names** match the bot role exactly as defined in the system — no abbreviations, no variations. If the bot is called "Copywriter" in the system, the file is `Copywriter_Knowledge_Base_v...`, not `CW_KB_v...` or `Copy_KB_v...`.

---

## Document Interaction Overview

```
┌─────────────────────────────────────────────────────────┐
│                    Claude Project                       │
│                                                         │
│  Custom Instructions:                                   │
│  ┌──────────────────────────────────────────────────┐  │
│  │  [Role]_Project_Instructions_v[X]_[Y].md         │  │
│  │  (loaded once, defines identity + behavior)      │  │
│  └──────────────────────────────────────────────────┘  │
│                                                         │
│  Knowledge Sources:                                     │
│  ┌──────────────────┐  ┌──────────────────────────┐   │
│  │  UNIVERSAL_CORE  │  │  [Role]_Knowledge_Base   │   │
│  │  v[X]_[Y].md     │  │  v[X]_[Y].md             │   │
│  │                  │  │                           │   │
│  │  (always loaded) │  │  Router → loaded at start │   │
│  │                  │  │  Sections → per query     │   │
│  └──────────────────┘  └──────────────────────────┘   │
│                                                         │
│  On-demand:                                             │
│  ┌──────────────────┐  ┌──────────────────────────┐   │
│  │  [Addon]         │  │  [Project_KB]            │   │
│  │  v[X]_[Y].md     │  │  v[X]_[Y].md             │   │
│  │  (task-specific) │  │  (engagement-specific)   │   │
│  └──────────────────┘  └──────────────────────────┘   │
└─────────────────────────────────────────────────────────┘
```

---

## Related Documents

- [architecture.md](./architecture.md) — system-level overview, bot roles, interaction model
- [roles-overview.md](./roles-overview.md) — per-bot role descriptions
- [../templates/](../templates/) — file templates for all four document types
