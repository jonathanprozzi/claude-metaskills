---
description: Interview-driven skill/command generator for domain experts
disable-model-invocation: true
---

# Skill Builder

A metaskill that interviews domain experts and generates Claude Code skills or slash commands from their tacit knowledge.

## What This Command Does

This command runs an interactive interview to:
1. Elicit tacit knowledge through conversation
2. Determine optimal format (skill vs slash command)
3. Generate the artifact with proper structure
4. Handle installation to the chosen destination

**Target user:** Someone who has expertise but doesn't know how to write Claude Code skills.

---

## Interview Flow

Run this interview conversationally. Don't rush through phases — let the expert share fully before moving on. Use adaptive depth: offer to go deeper, don't force it.

### Phase 1: Goal

Start with:

```
I'll help you package your expertise into a Claude Code skill or slash command.

What expertise or workflow do you want to package? What should Claude help with when using this?

Some examples:
- "Help builders think through product-market fit"
- "Review code for security vulnerabilities"
- "Guide someone through our onboarding process"
- "Analyze a PR for architectural concerns"
```

### Phase 2: Walkthrough

```
Walk me through how you actually do this.

- What questions do you ask?
- What do you look for?
- What's your mental process?
- Are there decision points where you go different directions?

I'll ask follow-up questions to understand the structure.
```

**Adaptive depth:** After their response, ask:
- "Want to go deeper on any part of this, or is that enough detail?"
- If they want depth → probe specific areas they mentioned
- If enough → acknowledge and move on

**Refinement branch:** After capturing their process, offer:

```
I've captured your process. Before we continue:

1. Package as-is → I'll structure exactly what you shared
2. Refine together → Let's improve the process before packaging
3. Get my suggestions → I'll share thoughts on structure/gaps, you decide what to keep
```

- If **Package as-is** → proceed to Phase 3
- If **Refine together** → collaborative back-and-forth to shape the process, then Phase 3
- If **Get my suggestions** → share observations (missing pieces, structure ideas, best practices), let them accept/reject, then Phase 3

This handles users who want help *thinking through* their process, not just capturing it.

### Phase 3: Context & References

```
What frameworks, mental models, or reference material do you use?

Do you have any documents or notes I should include?
- Paste content directly
- Share a link (I'll fetch it)
- Describe it and I'll help structure it
- Or skip if there's no reference material
```

**If material provided:** Read/fetch it, confirm understanding, note this signals SKILL format (needs multiple files).

### Phase 4: Examples

```
Can you give me an example of:

1. A GOOD outcome from applying this expertise — what does success look like?
2. A BAD outcome or common mistake to avoid — what should people watch out for?
```

### Phase 5: Analysis

**Internally determine skill vs command based on signals:**

| Signal | Points to |
|--------|-----------|
| Linear flow, same steps every time | **Command** |
| Branching logic, "it depends" answers | **Skill** |
| Has reference material to include | **Skill** |
| Quick checklist or template | **Command** |
| Should auto-trigger on certain contexts | **Skill** |
| Walks through a framework with steps | **Skill** with reference files |

**Present your analysis:**

```
Based on what you've shared, I recommend a [SKILL / SLASH COMMAND].

Here's why:
- [Key reasoning from signals]

The structure I'm seeing:
- Core framework: [decision tree / checklist / process]
- Reference material: [yes, will include / no]
- Estimated files: [1 for command / N for skill]

Does this capture your expertise correctly? Anything to adjust before I generate it?
```

### Phase 6: Generation

Generate the artifact based on recommendation:

**For Slash Command:** Single markdown file
**For Skill:** Folder with SKILL.md + optional reference.md + optional examples.md

Show the full generated content and ask:
```
Here's what I generated. Take a look — does this capture your expertise correctly?

[Show full content]

What would you like to do?
1. Ship it! → I'll save it now
2. Let me refine... → Tell me what to adjust
3. Show me the raw files → For manual copying
```

### Phase 7: Destination

**First, detect their setup:**

```bash
# Check if ~/.claude/commands/ has symlinks pointing to a dotfiles directory
ls -la ~/.claude/commands/ 2>/dev/null | grep "^l" | head -3
```

**Then adapt the flow:**

**If symlinks detected** (dotfiles workflow):
```
I see you manage commands in [detected dotfiles path] with symlinks.

Want me to:
1. Write to [dotfiles path] + create symlink → Works immediately, stays in your dotfiles
2. Write directly to ~/.claude/ → Simpler, but outside your dotfiles
3. Just show me → Display for manual copying
```

**If no symlinks** (direct workflow):
```
Where should I save this?

1. Personal → ~/.claude/[skills|commands]/[name]
2. Team/Org → [Ask for path, e.g., ~/projects/team-cc-utils]
3. Just show me → Display for manual copying
```

**For dotfiles + symlink:** Write to detected path, create symlink to ~/.claude/
**For personal:** Create directory if needed, write files directly
**For team:** Write to specified path, suggest git workflow
**For manual:** Display with copy-paste instructions

---

## Output Templates

**Key requirements from Anthropic best practices:**
- **Descriptions:** Third person ("Analyzes..." not "I help..."), include WHAT + WHEN
- **Skill names:** Gerund form, lowercase, hyphens only (e.g., `analyzing-code`, `reviewing-prs`)
- **SKILL.md:** Keep under 500 lines; use reference files for longer content
- **Conciseness:** Claude is smart — only add context it doesn't already have

### Slash Command Template

```markdown
---
description: [Third-person description]. Use when [trigger context].
---

# [Display Name]

[Core instructions synthesized from walkthrough]

## Process

[Step-by-step flow or decision tree from their mental model]

## Key Considerations

[Frameworks and mental models they mentioned]

## Examples

**Good outcome:** [From interview]

**Avoid:** [Common mistakes from interview]

<!-- Generated by /skill-builder -->
```

### Skill Template (SKILL.md)

```markdown
---
name: [gerund-kebab-case]
description: [Third-person what it does]. Use when [trigger context with key terms].
---

# [Display Name]

[Brief overview — when Claude should apply this skill]

## Core Process

[Main framework or decision tree from walkthrough]

## Guidelines

[Key principles from interview]

## Reference

- See `reference.md` for detailed frameworks
- See `examples.md` for good/bad examples

<!-- Generated by /skill-builder -->
```

**Naming examples:**
- Good: `reviewing-code`, `analyzing-spreadsheets`, `processing-pdfs`
- Avoid: `code-review`, `helper`, `utils`

### Reference File Template (if needed)

```markdown
# [Name] Reference

## Frameworks

[Detailed frameworks from interview]

## Mental Models

[How to think about this domain]

## External Resources

[Links or citations if provided]
```

### Examples File Template (if needed)

```markdown
# [Name] Examples

## Good Outcomes

[Success examples from interview]

## Common Mistakes

[What to avoid, failure modes]
```

---

## Design Principles

Follow these throughout the interview:

1. **Conversational** — This is an interview, not form-filling. Let them talk.
2. **Adaptive depth** — Offer to go deeper, don't force detail they don't have.
3. **Make the decision** — Don't ask "skill or command?" Determine from signals.
4. **Validate understanding** — Repeat back before generating. Get confirmation.
5. **Reduce friction** — Handle the installation, don't just dump files.
6. **Allow iteration** — "Ship it!" or "Let me refine..." — they choose.

---

## Notes

- This is the first metaskill in the [[Claude Metaskills]] family
- Generated artifacts can feed into [[Org Knowledge Harness - Research|Org Harness]]
- For very long reference material, summarize key points rather than including everything
- Include "Generated by /skill-builder" comment at end of generated files for provenance
