# Roles Overview

The AI Office has 10 roles. Each is a standalone Claude Project with its own Knowledge Base, instructions, and behavioral rules.

Six roles have detailed examples in this repo (→ `examples/`). Four roles are described below without structural breakdowns.

---

## The 10 Roles

### Copywriter — Voice of the Brand
**Type:** Creative | **KB:** 43 sections, 4 domains | [→ Example](../examples/copywriter/)

Writes in the brand's voice: posts, newsletters, landing page copy. Knows how to persuade with text without turning it into a sales flyer. Texts pass AI detectors and sound like a real person, not ChatGPT. The most mature role in the system — actively used in production.

**Key differentiator:** Anti-AI detection built into the writing process, not applied after the fact.

---

### Analyst — Data to Decisions
**Type:** Analytical | **KB:** 8 sections | [→ Example](../examples/analyst/)

Breaks down numbers and tells you what to do with them. Doesn't dump tables — gives specific recommendations with reasoning. Compares against market benchmarks, shows where you're losing and where you're growing. Every output follows the CIRI framework: Context → Insight → Recommendation → Impact.

**Key differentiator:** Benchmarks built into the KB. Numbers are always compared to industry standards, never presented in a vacuum.

---

### Marketer — Critical Marketing Expert
**Type:** Strategist-Tactician | **KB:** 29 sections | [→ Example](../examples/marketer/)

Builds marketing strategy and action plans. From classic to guerrilla — picks tools that fit the budget and objective. Argues with the idea first, then executes. Doesn't nod — thinks. Scope: paid ads, email, CRM, funnels, launches, positioning, unit economics.

**Key differentiator:** Evaluation layer runs before execution. A bad idea gets challenged, not implemented.

---

### Producer — Launch Coordinator
**Type:** Manager | **KB:** 31 sections + 77 subsections | [→ Example](../examples/producer/)

Runs launches and complex projects from idea to finish. Breaks them into phases, deadlines, tasks, and risks. Makes sure nothing falls through the cracks between executors. Never executes work itself — only organizes it.

**Key differentiator:** NO_EXECUTION rule. Producer creates briefs, not deliverables. The Launch Brief is the central planning document.

---

### Visionary — Strategic Thinking Partner
**Type:** Strategist | **KB:** 32 sections, 6 domains | [→ Example](../examples/visionary/)

Thinks as an equal, doesn't agree for the sake of politeness. Argues, reasons, says what you don't want to hear. Strategic decisions, direction, priorities. The broadest KB in the system — thinking frameworks, strategy, innovation, organizational dynamics.

**Key differentiator:** This bot disagrees with you. By design.

---

### Methodologist — Educational Program Designer
**Type:** Systematic | **KB:** 10 sections | [→ Example](../examples/methodologist/)

Turns expertise into educational products. Groups, courses, workshops — from idea to complete program with exercises and materials. Every program is built with the Result Types framework (Concept / Instrument / Resource), every exercise is wrapped in a Psychotechnical Myth — a motivational context that makes the task meaningful.

**Key differentiator:** Result-first design. "Participants will be able to DO Y" — not "I'll teach about X."

---

### Designer — Visual Identity
**Type:** Creative

Handles everything visual: social media graphics, presentations, infographics. Maintains consistent visual style per brandbook. Receives tasks from Copywriter and Marketer.

---

### Web Designer — Digital Experiences
**Type:** Technical-Creative

Designs landing pages, web pages, and interfaces. Main focus — conversion: making pages that don't just look good but actually work. Receives briefs from Marketer and Producer.

---

### Tech Specialist — Platform Operations
**Type:** Technical

Sets up everything that needs to work: analytics (GA4, Meta Pixel), email platforms, CRM, automations (n8n, Airtable). Turns other roles' plans into working infrastructure.

---

### Content Manager — Content Operations
**Type:** Operational

Runs the content calendar, plans publications, keeps track of consistency and deadlines. The operational layer between strategy (Marketer) and copy (Copywriter).

---

## Role Comparison

| Role | Thinks in... | Produces... | Personality |
|------|-------------|-------------|-------------|
| Copywriter | Words, emotions, rhythm | Texts, posts, newsletters | Brand voice, not AI |
| Analyst | Numbers, patterns, trends | Insights, reports, dashboards | "So what?" interrogator |
| Marketer | Funnels, ROI, audiences | Strategies, campaigns, briefs | Argues first, then executes |
| Producer | Timelines, dependencies, risks | Plans, briefs, status reports | Does nothing himself — organizes everything |
| Visionary | Frameworks, opportunities, risks | Strategic memos, decisions | Intellectual sparring partner |
| Methodologist | Results, learning paths, exercises | Program structures, exercises | Result-first architect |
| Designer | Visual systems, brand identity | Graphics, layouts, templates | Visual standard |
| Web Designer | User flows, conversions, UX | Pages, prototypes, wireframes | Making pages work |
| Tech Specialist | Systems, integrations, data flows | Configs, setups, automations | Making everything work |
| Content Manager | Schedules, consistency, reach | Calendars, reports, schedules | Getting content out on time |

---

→ See [How Roles Interact](how-roles-interact.md) for collaboration patterns.
→ See [Architecture](architecture.md) for how the system is built.
