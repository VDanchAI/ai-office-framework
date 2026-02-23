# AI Office Framework

**AI Agent Builder — assemble a bot team tailored to your tasks**

> From Claude to GPT — and beyond

> 10 roles. Unified architecture. Built on Claude Projects.

> 🇷🇺 [Русская версия](README.md)

---

## What is this?

AI Office is a framework for building a team of specialized AI bots, where each bot performs one role: writes copy, analyzes data, builds strategy, coordinates launches, designs training programs.

Each role is a separate Claude Project with a set of documents: knowledge base, behavioral instructions, navigation router. Together they form a virtual office.

**This is not a prompt collection.** This is an architecture — a system of documents, protocols, and navigation that turns AI from a "smart chatbot" into a specialist with deep expertise, defined personality, and strict constraints.

---

## How this differs from typical AI assistants

| | Typical approach | AI Office |
|---|---|---|
| Roles | One bot does everything | 10 specialized bots |
| Knowledge | Generic LLM knowledge | Hand-built KBs (1,000–27,000 lines per role) |
| Navigation | Full KB loaded into context | Router loads only the needed section |
| Behavior | "Helpful assistant" | Personality: argues, challenges, has opinions |
| Quality | Hope for the best | Self-check, iron rules, D.A.O.S. quality cycle |
| Collaboration | Manual copy-paste | Task handoffs via REQUEST format |

---

## Architecture

One role = one Claude Project with this document set:

```
┌─────────────────────────────────────────────┐
│  1. Universal Core                          │
│     Shared rules for ALL bots               │
│     Protocols: clarify, analyze, check      │
├─────────────────────────────────────────────┤
│  2. Project Instructions                    │
│     WHO this bot is (identity, boundaries)  │
│     HOW it behaves (iron rules)             │
│     WHAT it produces (output formats)       │
├─────────────────────────────────────────────┤
│  3. Knowledge Base + Router                 │
│     WHAT it knows (domain expertise)        │
│     Router = navigation (JSON)              │
│     Only the needed section is loaded,      │
│     not the entire KB                       │
├─────────────────────────────────────────────┤
│  4. Add-ons (optional)                      │
│     Extra knowledge per task                │
│     Brandbook, specifications, toolkits     │
└─────────────────────────────────────────────┘
```

### How it works

1. **Universal Core** is loaded into every project — shared rules for all bots
2. **Project Instructions** define behavior: personality, tone, format, constraints
3. **Knowledge Base** contains role-specific expertise (methods, techniques, examples)
4. **Router** (JSON inside KB) — navigation: finds the right section by user query and loads only that section
5. **Add-ons** — extra knowledge bases for specific tasks (brandbook, style guide, platforms)

> Details: [docs/en/architecture.md](docs/en/architecture.md)

### Brandbook

The Brandbook is an **add-on** attached to content and communication roles: Copywriter, Marketer, Designer.

What's inside:
- **Brand Voice** — tone, style, vocabulary, banned phrases
- **Visual Identity** — colors, fonts, logos, design principles
- **Platforms** — adaptation per channel (Telegram, Instagram, website, newsletters)
- **Identity** — mission, values, positioning

Modular system: 4 modules (Identity, Voice, Visual, Platforms), each with its own router. One brandbook — all bots speak with one voice. Customizable per client.

> Details: [docs/en/brandbook-structure.md](docs/brandbook-structure.md)

---

## Knowledge Base Navigation: Router

The key idea — the bot **doesn't load the entire KB**. Thousands of lines → lost focus, wasted tokens. Instead — a JSON router at the top of the KB:

```json
{
  "router_type": "flat",
  "total_sections": 6,

  "sections": [
    {
      "id": "S1",
      "title": "Section Name",
      "anchor": "#S1_SECTION_NAME",
      "triggers": ["keyword1", "keyword2", "phrase"],
      "description": "When to use this section",
      "priority": 10
    }
  ],

  "ai_instructions": {
    "routing_strategy": [
      "1. Analyze user query intent",
      "2. Match against section triggers",
      "3. Jump to anchor → read section → respond",
      "4. No match → use fallback"
    ]
  }
}
```

**Two router types:**

| Type | When | How it works |
|------|------|-------------|
| **Flat** | Up to ~20 sections | One lookup table, direct match |
| **Hierarchical** | 20+ sections | Master Router → domain → Sub-Router → section |

> Details: [docs/en/document-hierarchy.md](docs/document-hierarchy.md)

---

## Office Roles

### 6 roles with full structure (→ `examples/`)

| Role | Type | What it does |
|------|------|-------------|
| **Copywriter** | Creative | Writes in the brand's voice: posts, newsletters, landing page copy. Knows how to persuade with text without turning it into a sales flyer. Texts pass AI detectors and sound like a real person, not ChatGPT |
| **Analyst** | Analytical | Breaks down numbers and tells you what to do with them. Doesn't dump tables — gives specific recommendations with reasoning. Compares against market benchmarks, shows where you're losing and where you're growing |
| **Marketer** | Strategist-Tactician | Builds marketing strategy and action plans. From classic to guerrilla — picks tools that fit the budget and objective. Argues with the idea first, then executes. Doesn't nod — thinks |
| **Producer** | Manager | Runs launches and complex projects from idea to finish. Breaks them into phases, deadlines, tasks, and risks. Makes sure nothing falls through the cracks between executors. Never executes work itself — only organizes it |
| **Visionary** | Strategist | Thinks as an equal, doesn't agree for the sake of politeness. Argues, reasons, says what you don't want to hear. Strategic decisions, direction, priorities |
| **Methodologist** | Systematic | Turns expertise into educational products. Groups, courses, workshops — from idea to complete program with exercises and materials |

### 4 roles — description only

| Role | Specialization |
|------|---------------|
| **Designer** | Visual content, creatives, brandbook design |
| **Web Designer** | UI/UX, landing pages, conversion design |
| **Content Manager** | Content calendar, publishing, distribution |
| **Tech Specialist** | Platform setup, integrations, analytics |

> Details: [docs/en/roles-overview.md](docs/en/roles-overview.md) · [How Roles Interact](docs/en/how-roles-interact.md)

---

## Quick Start

### Build your own bot from templates

1. Copy templates from [`templates/`](templates/)
2. Define the role: who the bot is, what it does, what it does NOT do → `TEMPLATE_INSTRUCTIONS.md`
3. Fill the knowledge base with content → `TEMPLATE_KB.md`
4. Set up the router → JSON inside KB (flat) or `TEMPLATE_ROUTER.json` (hierarchical)
5. Copy Universal Core → `TEMPLATE_CORE.md`
6. Create a Claude Project → upload all files → test

> These are not ready-made bots — these are architecture descriptions for each role, so you can build your own.

> Step-by-step guide: [docs/en/deployment-guide.md](docs/en/deployment-guide.md)

### Explore examples

In [`examples/`](examples/) — 6 demo roles with full structural breakdown:
- What sections are in the knowledge base and why
- How instructions are structured (blocks, patterns, iron rules)
- What the router looks like (flat / hierarchical)

---

## Repository Structure

```
ai-office-framework/
│
├── README.md                          ← Russian version
├── README_EN.md                       ← You are here
│
├── docs/                              ← Architecture documentation (Russian)
│   ├── en/                            ← English versions
│   ├── architecture.md                ← System overview
│   ├── roles-overview.md              ← All 10 roles
│   ├── how-roles-interact.md          ← Interactions, REQUEST format
│   ├── document-hierarchy.md          ← Role document structure
│   ├── deployment-guide.md            ← Step-by-step bot assembly
│   └── brandbook-structure.md         ← Brandbook structure (4 modules)
│
├── templates/                         ← Blank templates for assembly
│   ├── TEMPLATE_CORE.md               ← Universal Core skeleton
│   ├── TEMPLATE_KB.md                 ← Knowledge Base skeleton + flat router
│   ├── TEMPLATE_INSTRUCTIONS.md       ← Instructions skeleton
│   ├── TEMPLATE_ROUTER.json           ← Hierarchical router (for 20+ sections)
│   └── TEMPLATE_ADDON.md              ← Add-on KB skeleton
│
├── examples/                          ← 6 demo roles (structure, not bots)
│   ├── copywriter/                    ← 43 sections, 4 domains, hierarchical
│   ├── analyst/                       ← 8 sections, CIRI framework
│   ├── marketer/                      ← 29 sections, evaluation layer
│   ├── producer/                      ← 31 sections + 77 subsections
│   ├── visionary/                     ← 32 sections, 6 domains
│   └── methodologist/                 ← 10 sections, result-first
│
└── assets/                            ← Diagrams and schemas
```

---

## Platform

The framework is built for **Anthropic Claude** (Projects). Adaptation to other platforms (ChatGPT, API-based systems) is possible — [get in touch](#contact).

---

## Want a ready-made office?

The templates and examples here are the architecture. The skeleton you can use to build your own bots.

If you need:
- **A ready-made bot** for your task — with polished prompts, knowledge base, and router
- **A full AI office** for your business — all roles, configured for you
- **A custom brandbook** — so all bots speak in your voice
- **GPT adaptation** — if you're not on Claude

> **[Get in touch](#contact)**

---

## License

[CC BY-NC 4.0](https://creativecommons.org/licenses/by-nc/4.0/) — Creative Commons Attribution-NonCommercial 4.0

Allowed:
- ✅ Study the architecture and approach
- ✅ Use templates to build your own bots
- ✅ Modify for your needs
- ✅ Share with attribution

Not allowed:
- ❌ Sell these materials as your own
- ❌ Use in commercial products without permission

---

## Contact

**Victor Danch (VDanch)** — AI marketing automation

- Telegram: [@vangogishe](https://t.me/vangogishe)
- Email: vikidanci@gmail.com
