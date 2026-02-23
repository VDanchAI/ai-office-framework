# Architecture

## What is an AI Office?

An AI Office is a system of specialized AI bots, each with a defined role, working together to cover the full scope of marketing and content operations. Instead of one general-purpose assistant that does everything poorly, you get 10 focused specialists that each do their domain well.

Each bot = one Claude Project with its own instructions, knowledge base, and behavioral rules. Together, they form a virtual team.

## Core Idea

**One bot per function. Deep expertise over broad coverage.**

A copywriter that actually writes like a human. An analyst that never delivers data without a recommendation. A marketer that argues against bad strategies before executing them. A visionary that tells you uncomfortable truths about your plans.

These aren't generic assistants with different names. Each bot has:
- Its own **Knowledge Base** (domain expertise, techniques, frameworks)
- Its own **Project Instructions** (behavioral rules, iron constraints, workflows)
- A shared **Universal Core** (common protocols all bots follow)
- Optional **Add-ons** (specialized knowledge loaded when needed)

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
│     Sections accessed by anchor, not loaded  │
│     in full                                 │
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
2. **Router** (JSON block at the top of the KB) maps the query to a section
3. **Bot jumps to that section** using its anchor
4. **Only that section is loaded** into context
5. **Bot generates a response** from that section + its instructions

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
- Project-level instructions persist across conversations
- Knowledge files are loaded into the project permanently
- Each project is isolated — bots don't leak into each other
- Memory persists across sessions within a project

**Adaptation to other platforms** (GPT, API-based systems) is possible but requires adjustments to the document loading mechanism and router implementation.

## What Makes This Different

| Approach | Typical AI setup | AI Office |
|----------|-----------------|-----------|
| Roles | One bot does everything | 10 specialized bots |
| Knowledge | Generic LLM knowledge | Curated KBs with 1,000-27,000 lines of domain expertise |
| Navigation | Full KB loaded (wasted context) | Router-based: load only what's needed |
| Behavior | "Helpful assistant" | Defined personality: argues, challenges, has opinions |
| Quality | Hope for the best | Self-check protocols, iron rules, D.A.O.S. quality cycle |
| Collaboration | Manual copy-paste | Structured handoffs with REQUEST format |

→ See [Roles Overview](roles-overview.md) for all 10 roles.
→ See [How Roles Interact](how-roles-interact.md) for collaboration patterns.
→ See [Deployment Guide](deployment-guide.md) to build your own.
