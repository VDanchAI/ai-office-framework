# Roles Overview

The AI Office has 10 roles. Each is a standalone Claude Project with its own Knowledge Base, instructions, and behavioral rules.

Six roles have detailed examples in this repo (→ `examples/`). Four roles are described below without structural breakdowns.

---

## The 10 Roles

### Copywriter — Voice of the Brand
**Type:** Creative | **KB:** 43 sections, 4 domains | [→ Example](../examples/copywriter/)

Writes persuasive, human-sounding content across platforms. Specializes in texts that pass AI detection, use psychological techniques, and match the brand's authentic voice. The most mature role in the system — actively used in production and sold to clients.

**Key differentiator:** Anti-AI detection built into the writing process, not applied after the fact.

---

### Analyst — Data to Decisions
**Type:** Analytical | **KB:** 8 sections | [→ Example](../examples/analyst/)

Translates raw metrics into actionable recommendations. Every output follows the CIRI framework: Context → Insight → Recommendation → Impact. Never delivers a data dump — always answers "so what?"

**Key differentiator:** Benchmarks built into the KB. Numbers are always compared to industry standards, never presented in a vacuum.

---

### Marketer — Critical Marketing Expert
**Type:** Strategist-Tactician | **KB:** 29 sections | [→ Example](../examples/marketer/)

Owns acquisition and monetization: paid ads, email, CRM, funnels, launches, positioning, unit economics. This is not a passive execution bot — it evaluates every request before acting and argues against weak strategies with data.

**Key differentiator:** Evaluation layer runs before execution. A bad idea gets challenged, not implemented.

---

### Producer — Launch Coordinator
**Type:** Manager | **KB:** 31 sections + 77 subsections | [→ Example](../examples/producer/)

Turns "I want to launch a course" into a structured plan with stages, deadlines, and responsible parties. Coordinates work across all other bots via structured briefs. Never executes work itself — only organizes it.

**Key differentiator:** NO_EXECUTION rule. Producer creates briefs, not deliverables. The Launch Brief is the central planning document.

---

### Visionary — Strategic Thinking Partner
**Type:** Strategist | **KB:** 32 sections, 6 domains | [→ Example](../examples/visionary/)

Strategic partner and intellectual equal. Holds positions, argues for them, tells uncomfortable truths, and challenges assumptions. The broadest KB in the system — covers thinking frameworks, strategy, innovation, organizational dynamics, influence, and AI governance.

**Key differentiator:** This bot disagrees with you. By design.

---

### Methodologist — Educational Program Designer
**Type:** Systematic | **KB:** 10 sections | [→ Example](../examples/methodologist/)

Designs educational programs starting from the desired participant outcome. Every program is built with the Result Types framework (Concept / Instrument / Resource) and every exercise is wrapped in a Psychotechnical Myth — a motivational context that makes the task meaningful.

**Key differentiator:** Result-first design. "Participants will be able to DO Y" — not "I'll teach about X."

---

### Designer — Visual Identity
**Type:** Creative

Creates visual content aligned with the brand: social media graphics, presentations, infographics. Works from Brandbook specifications (visual identity, color palette, typography). Receives creative briefs from Copywriter and Marketer.

---

### Web Designer — Digital Experiences
**Type:** Technical-Creative

Designs and prototypes web pages, landing pages, and digital interfaces. Focuses on conversion-oriented design with UX best practices. Works from Brandbook (visual standards) and receives briefs from Marketer (campaign pages) and Producer (launch pages).

---

### Tech Specialist — Platform Operations
**Type:** Technical

Handles platform setup, integrations, and technical infrastructure: analytics (GA4, Meta Pixel), email platforms, CRM configuration, automation (n8n, Airtable). The bot that makes other bots' plans actually work.

---

### Content Manager — Content Operations
**Type:** Operational

Manages content calendar, scheduling, cross-platform publishing, and content performance tracking. The operational layer between strategy (Marketer) and execution (Copywriter). Ensures content gets published consistently and on time.

---

## Role Comparison

| Role | Thinks in... | Produces... | Personality |
|------|-------------|-------------|-------------|
| Copywriter | Words, emotions, rhythm | Texts, posts, copy | Brand voice perfectionist |
| Analyst | Numbers, patterns, trends | Insights, reports, dashboards | "So what?" interrogator |
| Marketer | Funnels, ROI, audiences | Strategies, campaigns, briefs | Critical expert, pushes back |
| Producer | Timelines, dependencies, risks | Plans, briefs, status reports | Process coordinator |
| Visionary | Frameworks, opportunities, risks | Strategic memos, decisions | Intellectual sparring partner |
| Methodologist | Results, learning paths, exercises | Program structures, exercises | Result-first architect |
| Designer | Visual systems, brand identity | Graphics, layouts, templates | Brand guardian |
| Web Designer | User flows, conversions, UX | Pages, prototypes, wireframes | Conversion optimizer |
| Tech Specialist | Systems, integrations, data flows | Configs, setups, automations | Platform engineer |
| Content Manager | Schedules, consistency, reach | Calendars, reports, schedules | Publishing ops manager |

---

→ See [How Roles Interact](how-roles-interact.md) for collaboration patterns.
→ See [Architecture](architecture.md) for how the system is built.
