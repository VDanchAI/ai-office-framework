# AI Office Framework
**Build a team of experts. No hiring, contracts, or Friday meetings.**

---

## Why you need this

Anyone who builds something with their own hands — a product, a practice, an agency, a course — at some point realizes: you can't do it alone. You need someone who writes copy. Who thinks about strategy. Who handles content while you handle the work. Who reads numbers and won't let you get comfortable with pretty but meaningless metrics.

Hiring people is expensive. Freelancers disappear. Agencies charge for air.

AI Office solves this differently.

---

## What this is

Not a prompt collection. Not chatbots that answer "how can I help."

Each member of AI Office is a **digital expert**: a character with their own personality, their own area of expertise, their own way of thinking and arguing. The copywriter knows how persuasion works and why most texts fail. The analyst can read numbers in a way that produces decisions. The visionary won't nod along when you're wrong — and that's their main value.

Each of them works from a knowledge base: hundreds of pages of expertise on their subject, built by hand. Not the general knowledge of a language model — specific professional expertise within the role.

This is not a replacement for human relationships. This is a replacement for expensive, slow, and unreliable processes.

---

## Character examples

### Copywriter
Writes to be read. Knows the difference between text that persuades and text that irritates. Doesn't produce template "sales" constructs — works with psycholinguistics, rhythm, and subtext. Texts pass AI detectors and sound like a real human.

### Analyst
Takes numbers and tells you what to do with them. Doesn't dump tables — gives specific conclusions with explanations. Compares against market benchmarks. Shows where the real losses are, and where it's just an uncomfortable truth.

### Marketer
Builds strategy and action plans. First breaks the idea apart, then puts it back together. Doesn't nod — thinks. Picks tools for the actual budget and task, not the textbook.

### Producer
Runs projects and launches from idea to finish. Breaks them into phases, timelines, tasks, risks. Makes sure nothing falls through the cracks between people. Executes nothing themselves, only organizes — which is, in fact, the hardest part.

### Visionary
Thinks as an equal and doesn't agree out of politeness. If the idea is bad — will say so directly, with arguments and an alternative. Strategic decisions, direction, priorities. The kind you want around precisely because they're uncomfortable.

### Methodologist
Turns expertise into educational products. Groups, courses, workshops — from idea to a complete program with exercises and structure. If you have knowledge and don't know how to package it — here they are.

### Content Manager
Maintains the content calendar, tracks publications, manages distribution. Doesn't create — executes. The one who keeps the system moving when everyone else is busy with something else.

### Designer
Visual content, creatives, design. Knows what works on different platforms and why.

### Web Designer
UI/UX, landing pages, conversion design. Thinks not just about how it looks, but how it works.

### Tech Specialist
Platform setup, integrations, analytics. The one who makes all of this actually work.

---

These are out-of-the-box examples. But a character can be built for any task — accountant, lawyer, HR, technical writer, sales specialist. The architecture is the same, the content is anything.

---

## How this differs from typical AI assistants

|  | Typical approach | AI Office |
| --- | --- | --- |
| Roles | One bot for everything | 10 specialized characters |
| Knowledge | Generic LLM knowledge | Hand-built knowledge bases (1,000–27,000 lines per role) |
| Navigation | Full KB loaded into context | Router loads only the needed section |
| Behavior | "Helpful assistant" | Personality: argues, challenges, has opinions |
| Quality | Hope for the best | Self-check, iron rules, D.A.O.S. cycle |
| Coordination | Manual copy-paste | Task handoffs via REQUEST format |

---

## How it works

Each character is a separate Claude Project with a set of documents:

```
┌─────────────────────────────────────────────┐
│  1. Universal Core                          │
│     Shared rules for ALL characters         │
│     Protocols: clarify, analyze, check      │
├─────────────────────────────────────────────┤
│  2. Project Instructions                    │
│     WHO this character is (identity,        │
│     boundaries)                             │
│     HOW they behave (iron rules)            │
│     WHAT they produce (output formats)      │
├─────────────────────────────────────────────┤
│  3. Knowledge Base + Router                 │
│     WHAT they know (domain expertise)       │
│     Router = navigation (JSON)              │
│     Only the needed section is loaded,      │
│     not the entire KB                       │
├─────────────────────────────────────────────┤
│  4. Add-ons (optional)                      │
│     Brandbook, specifications, toolkits     │
└─────────────────────────────────────────────┘
```

**The router is the key thing.** Knowledge bases are large: 1,000–27,000 lines per role. Without navigation it's just a dump. The router works like a smart table of contents: receives a task, finds the right section, loads only that.

**Two router types:**

| Type | When | How it works |
| --- | --- | --- |
| **Flat** | Up to ~20 sections | One table, direct lookup |
| **Hierarchical** | 20+ sections | Master Router → domain → Sub-Router → section |

Example router (flat):

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

> More details: [docs/document-hierarchy.md](docs/document-hierarchy.md)

---

## Brandbook

The brandbook is an add-on that connects to roles working with content and communication: Copywriter, Marketer, Designer. One brandbook — all characters speak with one voice.

What's inside:
- **Brand Voice** — tone, style, vocabulary, banned phrases
- **Visual Identity** — colors, fonts, logos, design principles
- **Platforms** — adaptation per channel (Telegram, Instagram, website, newsletters)
- **Identity** — mission, values, positioning

Modular system: 4 modules (Identity, Voice, Visual, Platforms), each with its own router. Customizable per client.

> More details: [docs/brandbook-structure.md](docs/brandbook-structure.md)

---

## Quick Start

### Build your own character from templates
1. Copy templates from [`templates/`](templates/)
2. Define the role: who this character is, what they do, what they do **not** do → `TEMPLATE_INSTRUCTIONS.md`
3. Fill the knowledge base with content → `TEMPLATE_KB.md`
4. Set up the router → JSON inside KB (flat) or `TEMPLATE_ROUTER.json` (hierarchical)
5. Copy Universal Core → `TEMPLATE_CORE.md`
6. Create a Claude Project → upload all files → test

### Explore examples
In [`examples/`](examples/) — 6 demo roles with full structural breakdown:
- What sections are in the knowledge base and why
- How instructions are structured (blocks, patterns, iron rules)
- What the router looks like (flat / hierarchical)

> Step-by-step guide: [docs/deployment-guide.md](docs/deployment-guide.md)

---

## Two ways to use

**Build it yourself** — the repository has templates, architecture examples, and documentation. Take it, adapt it to your tasks, experiment. This is an open framework.

**Get it ready-made** — if you want to work rather than figure out the architecture: you can order ready-made characters for your project, or a complete system with setup and brandbook.

→ Telegram: [@vangogishe](https://t.me/vangogishe)
→ Email: vikidanci@gmail.com

---

## Repository structure

```
ai-office-framework/
│
├── docs/                    ← Architecture documentation
│   ├── architecture.md
│   ├── roles-overview.md
│   ├── how-roles-interact.md
│   ├── document-hierarchy.md
│   ├── deployment-guide.md
│   └── brandbook-structure.md
│
├── templates/               ← Templates for building your own character
│   ├── TEMPLATE_CORE.md
│   ├── TEMPLATE_KB.md
│   ├── TEMPLATE_INSTRUCTIONS.md
│   ├── TEMPLATE_ROUTER.json
│   └── TEMPLATE_ADDON.md
│
├── examples/                ← 6 demo roles with full structural breakdown
│   ├── copywriter/
│   ├── analyst/
│   ├── marketer/
│   ├── producer/
│   ├── visionary/
│   └── methodologist/
│
└── assets/
```

---

## Platform

Built for **Anthropic Claude** (Projects). Adaptation to other platforms is possible.

---

## License

[CC BY-NC 4.0](https://creativecommons.org/licenses/by-nc/4.0/)

You may study, use templates, modify for your own needs, and share with attribution. You may not sell this as your own or use it in commercial products without permission.
