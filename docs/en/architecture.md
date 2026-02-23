# Architecture

## What is an AI Office?

AI Office is a system of 10 specialized AI bots for marketing and content. Instead of one general-purpose assistant that does everything poorly — focused specialists, each deep in their domain.

Each bot = one Claude Project with its own instructions, knowledge base, and behavioral rules. Together, they form a virtual team.

## Core Idea

**One bot per function. Deep expertise over broad coverage.**

A copywriter that writes like a human. An analyst that never delivers numbers without a recommendation. A marketer that argues with the idea first, then executes. A visionary that says what you don't want to hear.

These aren't generic assistants with different names. Each bot has:
- Its own **Knowledge Base** (expertise, techniques, frameworks)
- Its own **instructions** (rules, constraints, workflows)
- A shared **core** (protocols for all bots)
- **Add-ons** (extra knowledge per task)

## The Document Stack

Every bot in the AI Office loads documents in this order:

```
┌─────────────────────────────────────────────┐
│  1. Universal Core                          │
│     Shared rules for ALL bots               │
│     Protocols: clarify, think, self-check   │
│     Communication rules, quality assurance  │
├─────────────────────────────────────────────┤
│  2. Project Instructions                    │
│     WHO this bot is (identity, scope)       │
│     HOW it behaves (iron rules, workflow)   │
│     WHAT it produces (output formats)       │
├─────────────────────────────────────────────┤
│  3. Knowledge Base + Router                 │
│     WHAT it knows (domain expertise)        │
│     Router = navigation system (JSON)       │
│     Only the needed section is loaded,       │
│     not the entire KB                       │
├─────────────────────────────────────────────┤
│  4. Add-ons (optional)                      │
│     Extra knowledge for specific tasks      │
│     Brandbook, platform specs, toolkits     │
│     Shared across bots when relevant        │
└─────────────────────────────────────────────┘
```

## Priority System

When sources conflict, higher priority wins:

| Priority | Source | Example |
|----------|--------|---------|
| 0 (highest) | User's current message | "Make it shorter" overrides everything |
| 1 | Universal Core | Shared protocols can't be overridden by individual bots |
| 2 | Bot Instructions | Role-specific rules override knowledge base content |
| 3 | User Preferences | Learned patterns from conversation history |
| 4 | Knowledge Base | Domain expertise |
| 5 (lowest) | Bot Judgment | Bot's own reasoning when nothing else applies |

## Router System

Bots don't load their entire Knowledge Base into context. That would waste tokens and dilute focus. Instead:

1. **User asks a question**
2. **Router** (JSON at the top of the KB) finds the needed section
3. **Bot loads only that section** into context
4. **Response is generated** from that section + instructions

Two router architectures:

| Type | When to use | How it works |
|------|-------------|-------------|
| **Flat** | Under 20 sections | One lookup table, direct match |
| **Hierarchical** | 20+ sections | Master Router → domain → Sub-Router → section |

→ See [Document Hierarchy](document-hierarchy.md) for details on how documents are structured.
→ See templates/ for router examples.

## Platform

The AI Office is built on **Claude Projects** (Anthropic). Each bot = one Claude Project.

**Why Claude Projects:**
- Instructions persist across conversations
- Knowledge files are loaded into the project permanently
- Projects are isolated — bots don't leak into each other
- Memory works across sessions within a project

Can be adapted to other platforms (GPT, API-based systems), but you'll need to rework document loading and router implementation.

## What Makes This Different

| Approach | Typical AI setup | AI Office |
|----------|-----------------|-----------|
| Roles | One bot does everything | 10 specialized bots |
| Knowledge | Generic LLM knowledge | Hand-built KBs (1,000–27,000 lines per role) |
| Navigation | Full KB loaded (wasted context) | Router loads only the needed section |
| Behavior | "Helpful assistant" | Personality: argues, challenges, has opinions |
| Quality | Hope for the best | Self-check, iron rules, D.A.O.S. quality cycle |
| Collaboration | Manual copy-paste | Task handoffs via REQUEST format |

→ See [Roles Overview](roles-overview.md) for all 10 roles.
→ See [How Roles Interact](how-roles-interact.md) for collaboration patterns.
→ See [Deployment Guide](deployment-guide.md) to build your own.
