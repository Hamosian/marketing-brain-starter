---
name: list-skills
description: Use this skill when the user asks to "list skills", "show skills", "what skills are available", "available skills", "skills list", "skill shortcuts", "show shortcuts", "what can you do", "what marketing skills do we have", "show me the skills", or wants an overview of all Marketing Brain workflows and how to trigger them. Always use this skill instead of summarizing from memory because the list is read live from the skills directory.
---

# List Available Skills

Show all skills available in this repo with natural trigger phrases and a one-line summary of what each does.

## How To Generate The List

1. Find all skill files: `.claude/skills/*/SKILL.md`.
2. Read each YAML frontmatter block.
3. Extract:
   - `name` - the skill identifier
   - `description` - trigger phrases and purpose
4. Distill each skill into:
   - **Trigger phrases:** 2-4 natural examples
   - **What it does:** one crisp sentence

## Output Format

Group skills by marketing operating domain:

```markdown
## Available Skills

### Daily Operations
| Skill | Say something like... | What it does |
|-------|-----------------------|--------------|
| `daily-brief` | "good morning", "morning brief" | Daily brief with active marketing work, blockers, Slack highlights, and next actions |

### Campaign & Work Intake
| Skill | Say something like... | What it does |
|-------|-----------------------|--------------|
| `marketing-os` | "run the marketing OS", "plan this campaign" | Routes broad marketing requests and synthesizes the next move |
| `marketing-brief` | "create a task", "write this up" | Turns requests into campaign-ready tracker briefs |

### Knowledge & Learning
...

### Specialist Workflows
...
```

Suggested groups:

- **Daily Operations** - briefs, standups, status checks
- **Campaign & Work Intake** - planning, triage, task creation, board processing
- **Knowledge & Learning** - interviews, retros, health checks, onboarding
- **Specialist Workflows** - CRM, paid, website, content, SEO, events, analytics, or system-specific skills

Create new groups when custom skills deserve them.

## Style Notes

- Keep trigger phrases natural and short.
- Avoid listing every phrase in the frontmatter.
- The "What it does" column should sound useful to a marketer, not like internal tooling jargon.
- Add this footer: "To trigger a skill, describe what you need. Exact phrases are not required."
- Include `list-skills` itself under Knowledge & Learning so users can find it again.
