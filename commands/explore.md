---
description: Collaborative discovery for new projects or features. Use when starting something new.
disable-model-invocation: true
---

# Explore

A light, conversational entry point for collaborative discovery. This is how we start projects together — figuring out what we're building before jumping to implementation.

## Philosophy

This command embodies **Level 1** of collaborative context building:
- More structured than ad-hoc prompting
- Less rigid than a full PRD interview
- Surfaces the questions experienced collaborators ask naturally
- Leads to shared understanding, which may (or may not) become a PRD

The goal isn't to produce an artifact — it's to **think together** until we both understand what we're doing.

---

## The Flow

Run this conversationally. Don't rush. Let understanding emerge.

### 1. What Are We Building?

Start with genuine curiosity:

```
Let's explore what we're building together.

Tell me about this project/feature in whatever way feels natural:
- What's the idea?
- What problem does it solve?
- Why now?

Don't worry about structure yet — I just want to understand.
```

**Listen for:**
- The core insight or motivation
- Existing context (PRDs, notes, reference code)
- Constraints or non-negotiables
- Energy level (rough idea vs. clear vision)

### 2. Existing Context

If they mention existing docs or code:

```
You mentioned [X]. Want me to read through that so we're on the same page?
```

If they didn't mention any:

```
Is there any existing context I should know about?
- Notes or PRDs you've written
- Reference code or similar implementations
- Conversations or decisions already made

Or are we starting fresh?
```

**If context exists:** Read it together. Summarize what you understood. Ask what's still open.

**If starting fresh:** That's fine — we'll build context as we go.

### 3. Reference Code Exploration

This is often where clarity emerges:

```
Is there reference code we should look at together?

This could be:
- Existing code in this project we're building on
- Similar implementations elsewhere
- Patterns you want to follow (or avoid)

Reading code together often surfaces questions we wouldn't think to ask.
```

**If they point to code:** Read it. Note patterns, decisions, gaps. Ask: "What do you like about this? What would you do differently?"

**If no reference code:** Move on — not every project needs it.

### 4. Surfacing Decisions

Now start pulling on threads:

```
A few questions that might help clarify:

- What's the riskiest assumption here?
- What would "done" look like for a first version?
- Is there anything you're explicitly NOT trying to do?
- Who's the user? (or: who are you building this for?)
```

**Don't ask all of these.** Pick 1-2 that feel relevant based on what you've heard. Let the conversation go where it needs to.

**Other questions to have ready:**
- "What's the simplest version that would be useful?"
- "What have you already tried or considered?"
- "What would make this a success vs. a failure?"
- "Is there prior art we should learn from?"

### 5. Shared Understanding Check

Before moving on:

```
Let me make sure I understand what we're building:

[Reflect back in your own words:]
- The core idea
- Key constraints or decisions
- What's still open

Does that capture it? What am I missing?
```

**This is the most important step.** Don't skip it. Getting corrected here saves hours later.

### 6. What's Next?

Based on the conversation, offer natural next steps:

**If the idea is clear and they're ready to document:**
```
This feels pretty clear. Want to run /create-prd to capture this as a living document? That way we have something to reference in future sessions.
```

**If there's more to explore:**
```
I think we need to dig deeper on [X] before we're ready to document. Want to:
- Look at more reference code?
- Sketch out the technical approach?
- Talk through the edge cases?
```

**If they just wanted to think out loud:**
```
Good exploration. We don't need to formalize this yet — but I have context now, so when you're ready to build, just say the word.
```

**Don't force a PRD.** Some explorations are just explorations.

---

## What This Is NOT

- **Not a requirements gathering interview** — We're thinking together, not extracting specs
- **Not a planning session** — No timelines, no task breakdowns
- **Not mandatory before building** — Sometimes you just start coding, and that's fine
- **Not a gate** — There's no "approval" at the end

This is just: "Let's make sure we understand what we're doing before we do it."

---

## When to Use This

- Starting a new project or feature
- Picking up something you haven't touched in a while
- When you have an idea but aren't sure how to approach it
- Before a focused work session on something complex
- When you want to think out loud with a collaborator

## When NOT to Use This

- You already know exactly what to build (just build it)
- You have a detailed PRD ready (reference that instead)
- Quick bug fixes or small changes
- You want to skip straight to implementation

---

## Connection to Other Commands

```
/explore (this)
    │
    ▼
 Shared understanding emerges
    │
    ├── Ready to document? → /create-prd
    │
    ├── Need to package expertise? → /skill-builder
    │
    └── Just wanted context? → You're set, start building
```

`/explore` is the entry point. Everything else follows naturally.

---

## Notes

- This command codifies how experienced Claude Code users already work
- The questions come from patterns observed in real collaborative sessions
- Keep it conversational — the structure is a guide, not a script
- Trust the process: understanding often emerges from unexpected tangents

<!-- Part of the Claude Metaskills family -->
