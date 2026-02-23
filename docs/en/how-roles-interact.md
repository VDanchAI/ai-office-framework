# How Roles Interact

See also: [architecture.md](./architecture.md) | [roles-overview.md](./roles-overview.md)

---

## 1. Interaction Model

Each role in the AI Office is an **independent Claude Project**. There is no automatic agent-to-agent communication. No role can call another role directly. No orchestration layer runs in the background.

The user is the orchestrator.

Workflow:
1. User opens Role A's Project, provides input, gets output
2. User copies relevant output (or a formatted REQUEST) to Role B's Project
3. Role B picks up from there

This design is intentional. Each role stays focused on its domain. Context crosses role boundaries only when the user decides it should — and only as much context as is needed.

---

## 2. The REQUEST Format

To make handoffs structured and unambiguous, each role generates a standardized REQUEST block when passing work to another role. The user copies this block into the receiving role's conversation.

```
## REQUEST
**From:** [Bot Name]
**To:** [Bot Name]
**Task:** [What needs to be done]
**Context:** [Why this is needed, what came before]
**Inputs:** [Deliverables from the sending bot]
**Output:** [What the receiving bot should produce]
**Deadline:** [When]
```

**Example:**

```
## REQUEST
**From:** Marketer
**To:** Copywriter
**Task:** Write landing page copy for the new course launch
**Context:** Campaign strategy approved. Target audience: online business owners, pain point is time. Positioning: "done in a week" transformation.
**Inputs:** Campaign brief (attached), audience profile, key messages list
**Output:** Full landing page copy — headline, subheadline, 3 benefit blocks, CTA, FAQ (5 items)
**Deadline:** 2026-02-25
```

The sending role produces the REQUEST as part of its output. The receiving role treats it as a complete task specification and proceeds without needing additional clarification.

---

## 3. Common Collaboration Patterns

### Content Creation Flow

```
Marketer
  |-- strategy + content brief
  v
Copywriter
  |-- written content
  v
Content Manager
  |-- scheduled, formatted, ready to publish
```

Marketer defines what to say and why. Copywriter writes it. Content Manager handles delivery.

---

### Course Launch Flow

```
Methodologist
  |-- program structure + learning outcomes
  v
Producer
  |-- launch plan + team delegation
  v
Marketer ──────────────────── Copywriter
  |-- campaign strategy         |-- sales page, emails
  v                             v
          Analyst
            |-- metrics tracking + post-launch report
```

Methodologist builds the product. Producer coordinates the launch. Marketer and Copywriter run in parallel on campaign and copy. Analyst closes the loop.

---

### Campaign Optimization

```
Analyst
  |-- performance data + insights
  v
Marketer
  |-- strategy adjustment
  v
Copywriter
  |-- new creative brief + revised messaging
```

Starts with data, ends with updated creative. No guessing.

---

### Strategic Pivot

```
Visionary
  |-- market analysis + strategic recommendation
  v
Marketer
  |-- new positioning + audience targeting
  v
Copywriter
  |-- new messaging framework + tone of voice
```

Used when direction changes — new niche, new offer, new market segment.

---

### Full Office Cycle

```
Visionary
  |-- direction + priorities
  v
Marketer
  |-- strategy + campaigns
  v
Producer
  |-- project plan + assignments
  v
Methodologist   Copywriter   Designer
  |-- content      |-- copy     |-- visuals
  v                v            v
          Content Manager
            |-- publishing schedule
            v
          Analyst
            |-- results + recommendations
            v
          Visionary  (loop)
```

This is the complete cycle for a product or campaign from strategic intent to measurement and back. Not every project needs every role — use what the task requires.

---

## 4. AI Office Map

The AI Office Map is a JSON configuration file loaded into every role's Project as a reference document.

It contains:
- All 10 roles with their names and short descriptions
- Each role's domain and primary responsibilities
- What inputs each role accepts and what outputs it produces
- When to use each role (trigger conditions)
- Which roles a given role typically hands off to

Every bot reads this map, which means every bot knows who else exists and where to redirect when a task falls outside its domain. A Copywriter receiving a request about analytics knows to redirect to the Analyst. A Producer receiving a strategic question knows to redirect to the Visionary or Marketer.

The map does not enable direct communication — it enables accurate redirection.

---

## 5. What This Means in Practice

**No single bot needs to know everything.**
Each role has a defined scope. Depth within that scope matters more than breadth across all scopes.

**Each bot stays focused on its domain.**
When a task arrives that belongs elsewhere, the bot says so and generates a REQUEST for the right role. It does not attempt to cover ground outside its expertise.

**Quality comes from depth, not breadth.**
A Copywriter that only writes copy — and does it with full concentration — produces better output than a generalist trying to do everything. Same for every role.

**The user is the conductor; bots are the orchestra.**
The user decides what gets done, in what order, and when context moves from one role to another. The bots execute with precision inside their lanes. The system produces coherent output because the user holds the overall view.
