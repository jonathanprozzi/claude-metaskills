# Claude Metaskills

**Metaskills** are skills that help create other skills. They solve the knowledge elicitation problem — helping domain experts discover and structure what they know for Claude Code.

## The Problem

Most people who want to create a Claude Code skill face two problems:

1. **They don't know the format** — What's a SKILL.md? What's the frontmatter?
2. **They don't know the decisions** — Should this be a skill or a command? Do I need reference files? What structure fits my knowledge?

Template-based tools solve problem #1. **Metaskills solve problem #2.**

## What's Included

### `/skill-builder` — The Core Metaskill

Interviews you about your expertise, identifies patterns, recommends skill vs command, and generates the artifact.

```
You → Run /skill-builder
     → Answer questions about your expertise
     → Get a generated skill or command
```

**Features:**
- Conversational interview flow (not form-filling)
- Refinement branch — collaborate on improvements before packaging
- Skill vs command recommendation based on your knowledge shape
- Detection-based destination (respects your dotfiles workflow)

### Examples

Commands and skills generated using `/skill-builder`:

| Example | Type | What It Does |
|---------|------|--------------|
| `/create-prd` | Command | Interview → structured PRD with fidelity detection |

## Installation

```bash
# Copy to your commands directory
cp commands/skill-builder.md ~/.claude/commands/

# Or symlink for easy updates
ln -s $(pwd)/commands/skill-builder.md ~/.claude/commands/skill-builder.md
```

## Usage

```bash
# In any Claude Code session
/skill-builder
```

Then answer the interview questions. The metaskill will:
1. Understand your expertise
2. Offer suggestions (if you want them)
3. Recommend skill vs command
4. Generate the artifact
5. Save to your preferred location

## Methodology

The metaskills approach is **tool-agnostic**. The patterns work across platforms:

- **Two-problem frame** — format vs decisions
- **Refinement branch** — capture vs collaborate vs suggest
- **Fidelity detection** — adapt depth to input
- **Skill vs command logic** — based on knowledge shape signals

Claude Code is the current implementation. The methodology ports to other AI coding tools.

## Validation

This approach is validated by how experienced Claude Code users already work. [Thariq (@trq212)](https://x.com/trq212/status/1873065033869750299), an Anthropic employee, shared a similar spec-based interview workflow (696K+ views).

The difference: his approach is ad-hoc prompting. Metaskills package the pattern so anyone can access it.

## Related

- [Anthropic Skills Repo](https://github.com/anthropics/skills) — official skills (no skill-builder)
- [Claude Code Skill Factory](https://github.com/alirezarezvani/claude-code-skill-factory) — template-based (different approach)

## License

MIT

---

*Built by [@jonathanprozzi](https://github.com/jonathanprozzi)*
