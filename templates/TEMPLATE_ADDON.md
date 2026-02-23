# [ADDON NAME] — [Bot Name] Add-on v1.0

**Version:** 1.0
**Date:** YYYY-MM-DD
**Purpose:** [What specialized knowledge this add-on provides]
**Scope:** [What it covers and what it does NOT cover]
**Parent KB:** [BotName]_Knowledge_Base_v[X].[Y].md

> Add-on KBs extend a bot's expertise in a specific area.
> They have their own Router and sections — same architecture as the main KB.
> The bot loads the Add-on's Router alongside the main KB Router.
> When a query matches an Add-on trigger, the bot reads the Add-on section.

<!--
  WHEN TO CREATE AN ADD-ON (vs adding sections to main KB):
  - Topic is deep enough to warrant 3+ sections
  - Topic is optional (not every user/project needs it)
  - Topic could be reused across multiple bots
  - Main KB is getting too large (1000+ lines)
  - You want to version this topic independently

  EXAMPLES:
  - Brandbook modules (Voice, Visual, Platforms) — loaded per bot
  - Platform-specific specs (LinkedIn rules, Facebook rules)
  - Methodology deep-dives (e.g., persuasion techniques toolkit)
  - Industry-specific knowledge (healthcare, fintech, etc.)
-->

---

## ROUTER

```json
{
  "kb_id": "[addon_short_name]",
  "version": "1.0",
  "last_updated": "YYYY-MM-DD",
  "parent_kb": "[BotName]_Knowledge_Base",
  "section_count": 4,
  "sections": [
    {
      "id": "S1_[TOPIC]",
      "title": "[Section 1 Title]",
      "anchor": "#S1_TOPIC",
      "triggers": ["trigger1", "trigger2", "trigger3"],
      "description": "What this section covers"
    },
    {
      "id": "S2_[TOPIC]",
      "title": "[Section 2 Title]",
      "anchor": "#S2_TOPIC",
      "triggers": ["trigger4", "trigger5", "trigger6"],
      "description": "What this section covers"
    },
    {
      "id": "S3_[TOPIC]",
      "title": "[Section 3 Title]",
      "anchor": "#S3_TOPIC",
      "triggers": ["trigger7", "trigger8"],
      "description": "What this section covers"
    },
    {
      "id": "S4_[TOPIC]",
      "title": "[Section 4 Title]",
      "anchor": "#S4_TOPIC",
      "triggers": ["trigger9", "trigger10"],
      "description": "What this section covers"
    }
  ]
}
```

---

## <a id="S1_TOPIC"></a>S1. [SECTION TITLE]

<!-- Your specialized content here -->

---

## <a id="S2_TOPIC"></a>S2. [SECTION TITLE]

<!-- Content -->

---

## <a id="S3_TOPIC"></a>S3. [SECTION TITLE]

<!-- Content -->

---

## <a id="S4_TOPIC"></a>S4. [SECTION TITLE]

<!-- Content -->

---

<!--
  ADD-ON TIPS:

  LINKING TO MAIN KB:
  - Reference main KB sections where relevant: "See also: Main KB → S5"
  - Don't duplicate content from main KB — reference it
  - Add-on sections can be referenced FROM main KB router too

  LOADING:
  - Bot loads Add-on Router alongside Main Router
  - If query matches Add-on trigger → bot reads Add-on section
  - If query matches both Main and Add-on → bot reads both
  - Add-on NEVER overrides Main KB — they complement each other

  SHARING ACROSS BOTS:
  - Same Add-on can be loaded into multiple bots
  - Example: Brandbook Add-on → loaded into Copywriter, Marketer, Designer
  - Each bot uses only the sections relevant to its role
  - Define in Bot Instructions which Add-on sections the bot should use

  VERSIONING:
  - Add-ons version independently from Main KB
  - Update Add-on version when its content changes
  - Main KB router may reference Add-on version for compatibility
-->

**END OF [ADDON NAME]**
