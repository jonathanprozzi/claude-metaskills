# Skills vs Commands: A Decision Guide

When you want to extend Claude Code, you have three main options: **skills**, **slash commands**, and **hooks**. This guide helps you choose.

## TL;DR

| Extension | Trigger | Use When |
|-----------|---------|----------|
| **Skill** | Automatic (Claude discovers) | "Claude should always know this" |
| **Command** | Manual (`/your-command`) | "I want to run this workflow" |
| **Hook** | Event-based (after tool calls) | "Do X whenever Y happens" |

**The key insight:** Skills are the edge case, not the default. Most knowledge works better as commands or conversation.

---

## The Decision Tree

```
Do you want Claude to apply this automatically, without you asking?
│
├─ YES → Is it contextual knowledge that varies by situation?
│        │
│        ├─ YES → SKILL (rare case)
│        │        Examples: domain expertise, coding standards, review criteria
│        │
│        └─ NO → Probably just a CLAUDE.md preference or system prompt
│
└─ NO → Do you want to trigger a specific workflow?
         │
         ├─ YES → COMMAND
         │        Examples: /checkpoint, /create-prd, /skill-builder
         │
         └─ NO → Should something happen after Claude takes an action?
                  │
                  ├─ YES → HOOK
                  │        Examples: auto-format after edits, notify on commits
                  │
                  └─ NO → You might not need an extension at all.
                          Try conversation + PRD as living document.
```

---

## Skills: The Rare Case

**What they are:** Markdown files in `~/.claude/skills/` that Claude automatically discovers and references.

**When to use:**
- Claude should apply this knowledge *without you asking*
- The knowledge is contextual — it depends on the situation
- You'd otherwise repeat this context in every session

**Signals in your language:**
- "It depends on..."
- "There are different approaches for different cases..."
- "Claude should just know that we..."

**Examples:**
- Security review criteria for your stack
- Domain-specific terminology in your industry
- Coding conventions Claude should always follow

**Why they're rare:** Most "always-on" knowledge is better captured in:
- `CLAUDE.md` (project-level preferences)
- System prompts (global preferences)
- PRDs (living documents Claude references naturally)

**The test:** Would it feel *wrong* if Claude forgot this mid-session? If yes, maybe a skill. If you'd just remind Claude, use a command or document.

---

## Commands: The Common Case

**What they are:** Markdown files in `~/.claude/commands/` that you invoke explicitly with `/command-name`.

**When to use:**
- You want to trigger a specific workflow
- The process has defined steps
- You control when it happens

**Signals in your language:**
- "I always do these steps..."
- "First I do X, then Y, then Z..."
- "When I want to [goal], I run through this process..."

**Examples:**
- `/checkpoint` — Save session state
- `/create-prd` — Interview + structured PRD
- `/skill-builder` — Interview + generate extension
- `/review-pr` — Run through review checklist

**Why they're common:** Most workflows are explicit. You know when you want to run them. Commands respect that.

---

## Hooks: The Automation Case

**What they are:** Shell commands that run automatically when Claude takes certain actions (tool calls, events).

**When to use:**
- You want side effects after Claude actions
- You'd otherwise manually run something every time
- The automation shouldn't require Claude's involvement

**Signals in your language:**
- "Every time Claude edits a file, I want..."
- "Whenever a commit happens, we should..."
- "After any session, make sure..."

**Examples:**
- Auto-format files after edits
- Log tool usage to a file
- Notify a channel on certain events
- Update a dashboard after checkpoints

**Why they're separate:** Hooks are *system-level* automation. They don't add knowledge — they add behavior.

---

## Common Mistakes

### "I'll make a skill for my workflow"

If you're describing steps, it's a command. Skills are knowledge, not processes.

```
Wrong: A skill that says "when doing code review, first check X, then Y..."
Right: A command /code-review that walks through X, then Y
```

### "I need a skill so Claude remembers this"

Claude reads project files, PRDs, and CLAUDE.md. You often don't need a skill — you need a well-structured document in your repo.

```
Wrong: A skill with project context
Right: A CLAUDE.md or PRD that Claude naturally references
```

### "I'll make a hook for complex logic"

Hooks are shell commands. If you need Claude's judgment, use a command instead.

```
Wrong: A hook that tries to do AI-powered analysis
Right: A command that Claude runs with your prompt
```

---

## Still Not Sure?

Ask yourself:

1. **Is this knowledge or workflow?**
   - Knowledge (contextual, varies) → Skill
   - Workflow (steps, sequence) → Command

2. **Who triggers it?**
   - Claude automatically → Skill
   - You explicitly → Command
   - System event → Hook

3. **Could conversation + documents handle it?**
   - Often yes. Extensions are for patterns you repeat *constantly*.

---

## The Meta-Point

Most people reaching for skills actually need commands. Most people reaching for commands actually need better PRDs. The `/skill-builder` metaskill helps you figure this out — it'll often recommend *against* building a skill.

The best extension is the one you don't build because your workflow already handles it.

---

*Part of the [Claude Metaskills](../README.md) methodology. For how these patterns emerged, see [methodology.md](methodology.md).*
