# [BOT_NAME] — Knowledge Base v1.0

**Version:** 1.0
**Date:** YYYY-MM-DD

> This is the Knowledge Base for your bot — the core repository of domain expertise.
> Structure: ROUTER (JSON, at the top) → Sections (content, accessed by anchor).
> The bot NEVER loads the entire KB. It reads the Router, finds the right section, jumps to it.

---

## ROUTER

<!--
  The Router is the navigation system for your KB.
  It maps user queries to specific sections using triggers (keywords/phrases).
  The bot reads ONLY this JSON block first, then jumps to the matched section.

  TWO ARCHITECTURE OPTIONS:

  FLAT (recommended for KBs under 20 sections):
    One router, all sections listed directly.

  HIERARCHICAL (for large KBs, 20+ sections):
    Master Router → domain groupings → Sub-Routers per domain.
    Each domain has its own section list.
    Routing: Stage 1 (which domain?) → Stage 2 (which section within domain?)

  This template shows FLAT architecture. See TEMPLATE_ROUTER.json for hierarchical.
-->

```json
{
  "router_version": "1.0.0",
  "router_type": "flat",
  "kb_name": "[BOT_NAME]_Knowledge_Base",
  "kb_version": "1.0",
  "total_sections": 6,
  "last_updated": "YYYY-MM-DD",

  "ai_instructions": {
    "routing_strategy": [
      "1. Analyze user query intent",
      "2. Match against section triggers (intent over exact keywords)",
      "3. If matched → jump to anchor, read section",
      "4. If multiple matches → read all matched sections",
      "5. If no match → use fallback"
    ],
    "fallback": "Route to S1 as the foundational section"
  },

  "sections": [
    {
      "id": "S1",
      "title": "Section 1 — [TOPIC]",
      "anchor": "#S1_TOPIC",
      "triggers": ["keyword1", "keyword2", "phrase one", "phrase two"],
      "description": "What this section covers (one sentence)",
      "priority": 10
    },
    {
      "id": "S2",
      "title": "Section 2 — [TOPIC]",
      "anchor": "#S2_TOPIC",
      "triggers": ["keyword3", "keyword4", "phrase three"],
      "description": "What this section covers",
      "priority": 8
    },
    {
      "id": "S3",
      "title": "Section 3 — [TOPIC]",
      "anchor": "#S3_TOPIC",
      "triggers": ["keyword5", "keyword6"],
      "description": "What this section covers",
      "priority": 6
    },
    {
      "id": "S4",
      "title": "Section 4 — [TOPIC]",
      "anchor": "#S4_TOPIC",
      "triggers": ["keyword7", "keyword8"],
      "description": "What this section covers",
      "priority": 6
    },
    {
      "id": "S5",
      "title": "Section 5 — [TOPIC]",
      "anchor": "#S5_TOPIC",
      "triggers": ["keyword9", "keyword10"],
      "description": "What this section covers",
      "priority": 4
    },
    {
      "id": "S6",
      "title": "Section 6 — [TOPIC]",
      "anchor": "#S6_TOPIC",
      "triggers": ["keyword11", "keyword12"],
      "description": "What this section covers",
      "priority": 4
    }
  ]
}
```

<!--
  ROUTER DESIGN TIPS:

  TRIGGERS:
  - Use both languages if your bot is bilingual
  - Include common misspellings and synonyms
  - Think about HOW users phrase requests, not just WHAT they ask
  - 5-10 triggers per section is a good range

  PRIORITY:
  - Higher number = checked first when multiple sections match
  - Foundational sections get highest priority (10)
  - Specialized sections get lower priority (4-6)

  ANCHORS:
  - Must match exactly: anchor in Router = heading ID in KB content
  - Format: #S[NUMBER]_SHORT_NAME (e.g., #S1_FOUNDATIONS)
  - Test every anchor after creating KB content

  SCALING:
  - Under 20 sections → flat router (this template)
  - 20-40 sections → consider hierarchical (group into 3-5 domains)
  - 40+ sections → definitely hierarchical + sub-routers
-->

---

<!-- ============================================================ -->
<!-- KB CONTENT — Each section accessed via its anchor              -->
<!-- ============================================================ -->

## <a id="S1_TOPIC"></a>S1. [SECTION TITLE — FOUNDATIONS]

<!--
  FIRST SECTION = Foundation of this role's expertise.
  This is the fallback section — bot routes here when nothing else matches.
  Make it comprehensive: core principles, key concepts, fundamental rules.
-->

### Core Principles

<!-- List 3-7 fundamental principles of this domain -->

1. **[Principle 1]** — [Brief explanation]
2. **[Principle 2]** — [Brief explanation]
3. **[Principle 3]** — [Brief explanation]

### Key Concepts

<!-- Define essential terms and concepts the bot needs to know -->

| Concept | Definition | When to Apply |
|---------|-----------|---------------|
| [Term 1] | [What it means] | [When the bot should use this] |
| [Term 2] | [What it means] | [When the bot should use this] |
| [Term 3] | [What it means] | [When the bot should use this] |

### Rules

<!-- Non-negotiable rules for this domain -->

- ALWAYS: [rule]
- ALWAYS: [rule]
- NEVER: [rule]
- NEVER: [rule]

---

## <a id="S2_TOPIC"></a>S2. [SECTION TITLE]

### [Subsection]

<!-- Your content here. Structure options:
  - Lists of techniques/methods
  - Tables with parameters
  - Step-by-step processes
  - Examples with annotations
  - Templates with fill-in sections
-->

### [Subsection]

<!-- Continue structuring content logically -->

---

## <a id="S3_TOPIC"></a>S3. [SECTION TITLE]

### [Subsection]

<!-- Content -->

---

## <a id="S4_TOPIC"></a>S4. [SECTION TITLE]

### [Subsection]

<!-- Content -->

---

## <a id="S5_TOPIC"></a>S5. [SECTION TITLE]

### [Subsection]

<!-- Content -->

---

## <a id="S6_TOPIC"></a>S6. [SECTION TITLE]

### [Subsection]

<!-- Content -->

---

<!--
  KB CONTENT TIPS:

  STRUCTURE EACH SECTION WITH:
  - Clear purpose (what does this section teach the bot?)
  - Actionable content (rules, techniques, templates — not theory)
  - Examples where possible (the bot learns from examples)
  - Cross-references to other sections when relevant: "See also: S3"

  WHAT MAKES A GOOD KB:
  - Bot can find any answer in 1-2 section jumps
  - Each section is self-contained (doesn't require reading other sections)
  - Content is prescriptive (DO this, NOT that) rather than descriptive
  - Examples show both good and bad outcomes

  VERSIONING:
  - Increment MINOR for content additions/edits (v1.0 → v1.1)
  - Increment MAJOR for structural changes (new sections, reorganization) (v1.1 → v2.0)
  - Update Router version when sections change
  - Keep changelog in Router JSON or at the end of this file

  SCALING:
  - KB getting large (1000+ lines)? → Split into domains, add Sub-Routers
  - Repeated content across sections? → Extract to a shared section, reference by anchor
  - Too many sections? → Group related ones into a domain, create Sub-Router
  - Need specialized depth? → Create Add-on KB (→ TEMPLATE_ADDON.md)
-->

**END OF [BOT_NAME] KNOWLEDGE BASE**
