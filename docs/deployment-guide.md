# Deployment Guide — How to Build Your Own Bot

This guide walks you through deploying one bot or an entire AI Office using the framework in this repo. Follow the steps in order. Skip nothing the first time through.

---

## 1. Prerequisites

Before you start building, make sure you have:

- **Claude Pro or Team account** — required for Claude Projects (the hosting mechanism for each bot)
- **Your domain expertise** — the bot amplifies what you already know; it cannot replace knowledge you don't have
- **A clear role and boundaries** — know what this bot does and, equally important, what it does not do

If you are unclear on the role, read `docs/architecture.md` first.

---

## 2. Step-by-Step: Building One Bot

### Step 1: Define the Role

Start here, not with content. A bot with a blurry role will drift and fail.

1. Write a **2-3 sentence role description** — who this bot is, what domain it covers
2. Write one **prime directive** — the single most important goal this bot exists to achieve
3. List **what the bot DOES** (5-10 concrete actions)
4. List **what the bot does NOT do** (at least 3 explicit exclusions)

> **Starting point:** `templates/TEMPLATE_INSTRUCTIONS.md`

**Tip:** If you cannot write the prime directive in one sentence, the role is not defined yet. Keep thinking.

---

### Step 2: Build the Knowledge Base

The KB is where the bot's expertise lives. Structure matters as much as content.

1. Identify **5-10 core topics** the bot needs to know to do its job
2. For each topic, write a section with:
   - The rule or principle
   - Why it matters
   - Actionable technique or checklist
   - One concrete example
3. Create a **Router** at the top of the KB — a JSON block that maps user query triggers to the right section
4. Use **anchors** to link Router entries to sections: `#S1_TOPIC_NAME`

**Router structure (flat, for up to ~20 sections):**

```json
{
  "router": [
    {
      "trigger": ["keyword1", "keyword2", "phrase"],
      "section": "#S1_TOPIC_NAME",
      "description": "When to use this section"
    }
  ]
}
```

> **Starting point:** `templates/TEMPLATE_KB.md`

> **When to switch:** If you reach 20+ sections, move to a hierarchical router. See `templates/TEMPLATE_ROUTER.json`.

**Warning:** A KB without a Router forces the bot to load everything on every query. This wastes tokens and degrades response quality. Always include the Router.

---

### Step 3: Write the Instructions

The Instructions file defines the bot's identity, behavior, and constraints. This is what goes into Claude's "Custom Instructions" field.

Fill in `templates/TEMPLATE_INSTRUCTIONS.md`. Pay close attention to these three sections:

| Section | What it controls | Getting it wrong costs you |
|---|---|---|
| **Identity** | Who the bot is, its voice and role | Role drift — bot tries to be everything |
| **Scope** | What the bot handles and what it refers elsewhere | Scope creep — bot does work it shouldn't |
| **Iron Rules** | Non-negotiable constraints, always followed | Unpredictable behavior, inconsistent output |

**Iron Rules guidance:**
- Aim for 5-10 rules (fewer = gaps, more = confusion)
- Each rule must be **testable** — you can look at a response and verify whether the rule was followed or broken
- Bad rule: "Be helpful" — not testable
- Good rule: "Never write copy without a defined target audience in the brief" — testable

**Always include a "Who You Are NOT" section.** List 3-5 roles this bot does not play. This single addition prevents most role drift issues.

---

### Step 4: Set Up Universal Core

The Universal Core is a shared file that goes into every bot in your office. It carries rules and protocols that apply everywhere.

1. Copy `templates/TEMPLATE_CORE.md`
2. Set your **language** (the language all bots communicate in)
3. Define your **communication style** (tone, format preferences, response length defaults)
4. Configure **quality protocols** (self-check steps the bot runs before responding)
5. Add any **org-wide constraints** that apply to all roles

> If you are building only one bot, the Universal Core still matters — it gives you a clean separation between role-specific rules (Instructions) and universal rules (Core).

---

### Step 5: Create the Claude Project

1. Go to **Claude → Projects → New Project**
2. Name the project after the bot's role (e.g., "Copywriter", "Analyst")
3. Paste your completed Instructions into the **"Custom Instructions"** field
4. Upload files to the project:
   - `universal-core.md` (required)
   - Your Knowledge Base file (required)
   - Any Add-on files relevant to this role (optional)
5. Run **5+ real queries** — queries you would actually send in production

**Tip:** Use queries that cover edge cases, not just ideal cases. Test the boundaries on the first pass.

---

### Step 6: Test and Iterate

Run each of these checks before calling the bot production-ready:

| Test | What to check | Fix if failing |
|---|---|---|
| **Router test** | Does the bot find and load the right KB section? | Add or tighten trigger keywords in Router |
| **Constraint test** | Does the bot follow every Iron Rule? | Rewrite vague rules to be testable |
| **Boundary test** | Does the bot stay in scope and decline out-of-scope requests? | Strengthen "Who You Are NOT" and Scope section |
| **Delegation test** | Does the bot hand off correctly to other roles? | Add or fix handoff triggers and REQUEST format |
| **Quality test** | Is output quality consistent across query types? | Improve self-check steps in Universal Core |

Iterate in this order: adjust triggers → tighten rules → add examples → re-test. Do not add more content until the Router and Iron Rules are working correctly.

---

## 3. Scaling to Multiple Bots (AI Office)

Building an AI Office is an additive process. Do not try to design the whole system upfront.

**The sequence that works:**

1. **Build one bot.** Get it working well. Ship it. Use it.
2. **Add a second bot** with a clearly defined boundary from the first. Document which queries go where.
3. **Create the Universal Core** — extract the rules that apply to both bots, centralize them. Both bots now share this file.
4. **Add the AI Office Map** — a JSON file listing all active roles, their prime directives, and when to route to each. See [how-roles-interact.md](how-roles-interact.md) for the AI Office Map concept.
5. **Build handoff protocols** — define the REQUEST format bots use when delegating to each other. Consistent format prevents broken handoffs.
6. **Add more bots one at a time.** Test each new handoff path before adding the next bot.

**Tip:** The AI Office Map becomes the navigation layer for the whole system. Keep it updated every time you add a role.

---

## 4. Common Mistakes

These are the failure modes that appear most often. Read them before you build, not after.

**1. Starting with content, not role definition**
You write 2,000 words of KB content before deciding what the bot's prime directive is. The content ends up scattered and the Router cannot organize it.
Fix: Define role, prime directive, and scope first. Start the KB only after Step 1 is locked.

**2. Making the KB too broad**
You try to cover everything tangentially related to the role. The bot becomes a generalist with shallow knowledge.
Fix: Deep expertise in a narrow domain beats wide coverage. Cut any section that is not essential to the prime directive.

**3. No Router**
The bot loads the entire KB on every query. Token usage is high, responses are slow, and relevance drops.
Fix: Always include a Router. Even a 3-section KB benefits from one. It is not optional.

**4. Vague Iron Rules**
Rules like "be professional" or "give good advice" sound reasonable but cannot be enforced.
Fix: Rewrite every Iron Rule so you can look at a response and say definitively: followed or broken. If you cannot do that, the rule needs rewriting.

**5. No "Who You Are NOT" section**
Without explicit exclusions, the bot attempts tasks outside its scope — slowly at first, then consistently.
Fix: Add at least 3 explicit "I am not a \_\_\_, I do not do \_\_\_" statements to the Instructions.

**6. Skipping the self-check protocol**
The bot produces output without reviewing it against quality criteria.
Fix: Add a self-check section to Universal Core. Even a 3-step check (accuracy, tone, completeness) measurably improves output consistency.

**7. Too many bots too fast**
You design 6 bots before the first one is working. Handoffs break, roles overlap, and debugging is a nightmare.
Fix: One bot, fully working, in real use. Then a second. Then a third. The compounding value of the office only appears when each component is solid.

---

## 5. Recommended Build Order

If you are building a full AI Office from scratch, this order delivers the fastest path to value:

| Priority | Role | Why this order |
|---|---|---|
| 1 | **Copywriter** | Highest immediate ROI — content production is always needed, results are visible fast |
| 2 | **Marketer** | Adds strategy layer to the content the Copywriter produces; the two roles amplify each other |
| 3 | **Analyst** | Measures what the first two produce; closes the feedback loop |
| 4 | **Producer** | Coordination becomes valuable once you have 3+ roles to coordinate |
| 5+ | Remaining roles | Add based on your actual bottlenecks, not a theoretical org chart |

**Warning:** Do not add the Producer before you have multiple bots running. A coordinator with nothing to coordinate is wasted effort.

---

## 6. Quick Reference

| I want to... | Start with... | Template to use |
|---|---|---|
| Build one bot | Steps 1-6 in Section 2 | `TEMPLATE_KB.md` + `TEMPLATE_INSTRUCTIONS.md` |
| Build a full AI Office | Section 3 (scaling sequence) | All templates + `TEMPLATE_CORE.md` |
| Add a specialty to an existing bot | Add-on file for that specialty | `TEMPLATE_ADDON.md` |
| Scale a large KB (20+ sections) | Hierarchical router | `TEMPLATE_ROUTER.json` |
| Debug a bot that drifts | Constraint and boundary tests (Section 2, Step 6) | Review `TEMPLATE_INSTRUCTIONS.md` Iron Rules |
| Set up shared rules across bots | Universal Core (Section 2, Step 4) | `TEMPLATE_CORE.md` |

---

## Related Documentation

- [architecture.md](architecture.md) — how the framework components fit together
- [document-hierarchy.md](document-hierarchy.md) — deep dive on document structure and Router design
- [roles-overview.md](roles-overview.md) — all 10 roles and their specializations
- [how-roles-interact.md](how-roles-interact.md) — collaboration patterns and REQUEST format
- `templates/TEMPLATE_INSTRUCTIONS.md` — instructions template with inline comments
- `templates/TEMPLATE_KB.md` — flat KB template with Router example
- `templates/TEMPLATE_CORE.md` — Universal Core template
- `templates/TEMPLATE_ADDON.md` — Add-on module template
- `templates/TEMPLATE_ROUTER.json` — hierarchical router for large KBs
