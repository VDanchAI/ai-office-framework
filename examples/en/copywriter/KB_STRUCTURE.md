# Copywriter — Knowledge Base Structure

> This document describes HOW the Copywriter's Knowledge Base is organized.
> It shows section names, their purpose, and domain groupings.
> The actual content (techniques, formulas, examples) is not included.

## Architecture: Hierarchical Router

The KB uses a **hierarchical router** (Master + Sub-Routers) because it has 43 sections.

```
Master Router
    ├── CORE_COPYWRITING (26 sections, priority: 10)
    │   └── Sub-Router: core_copywriting_router
    ├── NARRATIVE_THERAPY (6 sections, priority: 8)
    │   └── Sub-Router: narrative_therapy_router
    ├── PERSUASION (6 sections, priority: 7)
    │   └── Sub-Router: persuasion_router
    └── RHETORICAL_MASTERY (5 sections, priority: 6)
        └── Sub-Router: rhetorical_mastery_router
```

**Routing flow:**
1. User asks a question
2. Master Router → determines which domain
3. Sub-Router → finds exact section within that domain
4. Bot jumps to section anchor → reads content → generates response

---

## Domain 1: CORE_COPYWRITING (26 sections)

The foundation. Covers everything from writing style to platform specifications.

| Section | Title | Purpose |
|---------|-------|---------|
| S1 | River Syntax | Author's signature writing rhythm and sentence structure |
| S2 | Humanization | Techniques for making AI-generated text sound human |
| S3 | Three Registers | Formal / conversational / intimate voice switching |
| S4 | Forbidden Vocabulary | Words and phrases the bot must never use |
| S5 | Two-Layer Communication | Surface message + subtext layer |
| S6 | Addressing Rules | How to address the reader (tone, pronouns) |
| S7 | Self-Check Sequence | Quality verification before delivering text |
| S8 | Chekhov Style | "Subtraction" writing — say more with less |
| S10 | Hook Formulas | Opening lines that capture attention |
| S11 | Storytelling Frameworks | Narrative structures for posts and articles |
| S12 | Persuasion Techniques | Core persuasion mechanics in text |
| S13 | Emotional Triggers | Activating specific emotions through writing |
| S14 | Post Formats | Structural templates for different post types |
| S15 | CTA Formulas | Call-to-action patterns and placement rules |
| S16 | AI Detection Mechanics | How AI detectors work (to avoid detection) |
| S17 | AI Sentence Patterns | Patterns that flag text as AI-generated |
| S18 | Literary Masters | Writing techniques borrowed from literature |
| S19 | Spontaneous Speech Markers | Markers that simulate natural human speech |
| S20 | Psycholinguistics | Language influence techniques |
| S21 | Russian Style Fundamentals | Russian-specific writing rules and patterns |
| S22 | Russian Literary Masters | Techniques from Russian literary tradition |
| S23 | LinkedIn — Specifications | Character limits, fold rules, hashtag rules |
| S24 | LinkedIn — Formats | Post format templates and writing rules |
| S25 | LinkedIn — Soft Selling & CTA | Non-aggressive selling techniques for LinkedIn |
| S26 | Platform Restrictions | Content policy rules per platform |
| S46 | Copy Fundamentals | Foundational copywriting principles |

---

## Domain 2: NARRATIVE_THERAPY (6 sections)

Therapeutic writing techniques adapted for marketing. Creates deeper emotional connection.

| Section | Title | Purpose |
|---------|-------|---------|
| S27 | Externalization | Separating person from problem in narrative |
| S28 | Re-authoring | Helping reader rewrite their story |
| S29 | Unique Outcomes | Finding exceptions to the problem narrative |
| S30 | Alternative Storylines | Building new narratives from unique outcomes |
| S31 | Thick vs Thin Description | Rich, multi-layered storytelling vs reductive labels |
| S32 | Narrative Maps | Structured templates for therapeutic narratives |

**Each section includes:** Theory, process, language patterns, use cases, common mistakes.

---

## Domain 3: PERSUASION (6 sections)

Psychology-based influence techniques for ethical persuasion in text.

| Section | Title | Purpose |
|---------|-------|---------|
| S33 | Cialdini's 7 Principles | Reciprocity, commitment, social proof, authority, liking, scarcity, unity |
| S34 | Trust Building | Vulnerability + authority balance, credibility markers |
| S35 | Anti-Marketing | Selling through philosophy, indirect conversion |
| S36 | Emotional Triggers | FOMO, validation, intellectual pleasure, belonging, hope |
| S37 | Cognitive Biases | Memory, perception, social, decision, and emotional biases |
| S38 | Conversion Psychology | Micro-conversions, friction reduction, momentum building |

---

## Domain 4: RHETORICAL_MASTERY (5 sections)

Classical and modern rhetoric techniques adapted for digital content.

| Section | Title | Purpose |
|---------|-------|---------|
| S39 | Provocative Therapy | Exaggeration, reverse psychology, paradoxical intention |
| S40 | Analogies & Metaphors | Structural analogies, extended metaphors, cross-domain mapping |
| S41 | Rhetorical Questions | Erotesis, Socratic method, leading questions |
| S42 | Classical Rhetoric Devices | Ethos/Pathos/Logos, anaphora, antithesis, chiasmus, tricolon |
| S43–S45 | Advanced Rhetoric | Paradox & irony, framing & perspective, semantic precision |

---

## External Files (Add-ons)

The Copywriter's KB references external specialist files loaded separately:

| Add-on | Purpose | Loaded When |
|--------|---------|-------------|
| Social Media Specs | Platform-specific character limits, fold rules, format rules | Writing for LinkedIn/Facebook/Telegram |
| Russian Style Anti-AI Guide | Deep humanization techniques for Russian text | Every Russian text |
| Milton Model Toolkit | Hypnotic language patterns (Ericksonian hypnosis) | Persuasive / therapeutic writing |
| Psycholinguistics Toolkit | NLP-based influence techniques | Influence-heavy content |
| Platform Restrictions | Content policy rules | Platform-specific writing |

---

## Scaling Notes

This KB grew from 8 sections (v1.0) to 43 sections (v11.2) over multiple iterations:

- **v1–v5:** Flat router, single domain, basic copywriting
- **v6:** Switched to hierarchical router, added Narrative Therapy domain
- **v7:** Added Persuasion domain
- **v8:** Added Rhetorical Mastery domain
- **v10:** Extracted Milton Model to standalone file (Hub Model)
- **v11:** Current production version

**Key lesson:** Start flat, go hierarchical when you hit ~20 sections. Extract deep topics to Add-ons when a domain gets too large.
