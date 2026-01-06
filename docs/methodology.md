# Methodology: How We Work Together

This document captures the collaboration philosophy behind the metaskills in this repo. It's not a prompt guide — it's an explanation of *how* and *why* human-Claude collaboration works well.

## The Centaur Model

The "centaur" framing comes from [Ethan Mollick's research](https://www.oneusefulthing.org/p/centaurs-and-cyborgs-on-the-jagged) on AI and work. In his terminology:

- **Centaurs** divide labor strategically — human handles X, AI handles Y, with a clear boundary
- **Cyborgs** integrate deeply — intertwining work throughout, moving back and forth across tasks

Our workflow is closer to **cyborg** in Mollick's terms: continuous dialogue, generative conversation, thinking *together* rather than dividing tasks. But "centaur" has become the broader umbrella term for human+AI collaboration, and we use it that way here.

These metaskills emerge from that collaboration style:

- **Human brings:** Domain expertise, taste, judgment, context, goals — and crucially, *tacit knowledge* that can't be prompted out directly
- **Claude brings:** Structural patterns, synthesis, gap-detection, articulation — and the ability to *reflect back* what it's hearing so the human can correct

Neither is "driving" — it's genuine pair work. The human isn't just prompting; Claude isn't just executing. We're thinking together.

### Generative vs Extractive

The key insight: the conversation is **generative**, not extractive. New understanding emerges from dialogue that neither party had before.

This is different from requirements gathering, where you're pulling information out of someone's head. In centaur work, the questions themselves create new clarity.

| Extractive | Generative |
|------------|------------|
| "What are the requirements?" | "What's alive for you right now?" |
| "List the features" | "What would make this a success?" |
| "Who's the stakeholder?" | "Why does this matter to you?" |

Ask questions that invite reflection, not just recall.

## Core Principles

### 1. Collaborative Refinement > Pure Extraction

The temptation with AI is to treat it as an extraction tool: "capture what I know and format it."

Better: "Help me discover what I know, challenge my assumptions, suggest improvements."

This is why `/skill-builder` has a refinement branch:
```
1. Package as-is → I'll structure exactly what you shared
2. Refine together → Let's improve the process before packaging
3. Get my suggestions → I'll share thoughts, you decide what to keep
```

Option 3 is where the magic happens. The human gets to see patterns they couldn't see, while retaining full control over what to accept.

### 2. Meet Them Where They Are (Fidelity Detection)

Not every input needs the same treatment:

| Input Fidelity | Approach |
|----------------|----------|
| Rough idea | More discovery, help shape the vision |
| Medium detail | Clarify, battletest, then structure |
| Detailed spec | Light validation, focus on gaps/risks |

This is why `/create-prd` detects fidelity and adapts. The metaskill doesn't impose a fixed process — it reads the situation.

### 3. Battletest Before Committing

Before structuring anything, stress-test it:
- What could go wrong?
- What's the riskiest assumption?
- Is this scope realistic?
- What are we missing?

This surfaces problems early, when they're cheap to fix. It's not skepticism — it's collaborative rigor.

### 4. Living Documents Over Static Specs

A PRD isn't done when it's written. It evolves as understanding deepens.

This is why our PRDs have:
- **Session Handoff** sections (explicit context for continuity)
- **Open Questions** (unknowns we're tracking)
- **Updated annotations** (inline notes when decisions change)

The document is a thinking tool, not just an artifact.

### 5. Cyclical Refinement (Explore ↔ PRD)

The commands aren't a waterfall. They're tools you return to:

```
/explore
    │
    ▼
PRD captures current understanding
    │
    ▼
Build, learn, context shifts
    │
    ▼
/explore again (even on existing PRD)
    │
    ▼
PRD evolves with new tacit knowledge
    │
    ▼
(repeat as understanding deepens)
```

**Key insight from testing:** Running `/explore` on a project with an existing comprehensive PRD *still* surfaced tacit knowledge that wasn't captured — the "why" behind the "what," friction points, identity framing. The PRD had the decisions; explore surfaced the philosophy.

This means:
- `/explore` isn't just for new projects
- PRDs are never "done" — they're snapshots of current understanding
- The cycle is: explore → document → build → explore again

### 6. The Two-Problem Frame

Most people who want to package expertise face two problems:

1. **Format** — What's the structure? What's the syntax?
2. **Decisions** — What *should* this be? What shape fits my knowledge?

Templates solve #1. Metaskills solve #2.

The insight: the decisions are the hard part. Knowing *what* to build matters more than knowing *how* to write it.

## Patterns in Practice

### The Interview Pattern

Don't ask "what do you want?" — ask questions that surface tacit knowledge:
- "Walk me through how you actually do this"
- "What do you look for? What's your mental process?"
- "What's a good outcome look like? A bad one?"

Then reflect back: "Here's what I'm hearing..." — and let them correct.

### The Signal-Reading Pattern

Instead of asking "do you want X or Y?", detect from context:

| Signal | Interpretation |
|--------|----------------|
| "It depends on..." | Needs branching logic (skill, not command) |
| "I always do these steps..." | Linear flow (command, not skill) |
| "Here's a doc I reference..." | Needs multi-file structure |

Make the recommendation, explain why, let them override.

### The Handoff Pattern

Every substantial piece of work should be pickupable by a fresh session:
- What's the current state?
- What decisions have been made?
- What's the next action?
- What's explicitly out of scope?

This respects context limits and enables true continuity.

## Why This Matters

The metaskills aren't magic prompts. They're codified versions of collaboration patterns that work.

When someone asks "how do you work with Claude?" — the answer isn't a prompt template. It's:
- A philosophy (centaur collaboration)
- A set of principles (refinement, fidelity, battletest)
- Patterns that embody those principles (metaskills)

The metaskills make the patterns accessible. But the thinking behind them is what actually matters.

---

*This methodology emerges from ongoing collaboration between [@jonathanprozzi](https://github.com/jonathanprozzi) and Claude. It's descriptive, not prescriptive — these are patterns we've found work well, not rules.*
