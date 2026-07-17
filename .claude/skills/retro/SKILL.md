---
name: retro
description: Use this skill when the user wants to capture learnings from a completed campaign, launch, channel test, reporting cycle, workflow, platform change, or triage session. Triggered by "let's retro", "capture what we learned", "save this for next time", "update the skill", "what did we learn", "document this for next time", "don't forget this", or "we should remember this". Also suggest it proactively after novel or complex marketing work.
---

# Retro - Capture Marketing Learnings

This skill closes the learning loop. After a campaign, workflow, launch, or investigation, it captures what was learned and commits it to the repo so the next marketer starts with better context.

**When to use retro vs curious-intern:** Retro is reactive - something just happened and should be captured quickly. Curious-intern is proactive - the user has spare time and wants Claude to interview them for broader gaps.

## Step 1: Interview

Ask these together, skipping any that are already obvious from the conversation:

1. **What did we just do?** Include campaign, channel, platform, or workflow.
2. **What was surprising or non-obvious?** Capture the thing another teammate would trip on.
3. **What should Claude know next time?** The shortcut, caveat, approval rule, source, or "do not do X".
4. **Did any existing skill or doc give stale or incomplete guidance?** If yes, name it.

## Step 2: Route The Learning

| What was learned | Where it goes | Action |
|-----------------|---------------|--------|
| Platform behavior, campaign risk, workflow quirk, or failure mode | `systems/owned/<system>.md` | Add to the relevant section |
| Launch checklist or repeatable workflow improvement | `.claude/skills/<name>/SKILL.md` or `knowledge/` | Update the skill |
| Missing step, wrong assumption, or platform fallback | `.claude/skills/<name>/SKILL.md` | Fix the instruction |
| Partner handoff, approval rule, or team convention | `CLAUDE.md` or `references/` | Add the durable rule |
| Stale board ID, channel ID, dashboard link, or owner | The file that contains it | Fix directly |
| Personal preference | Memory | Only if it applies to one user and not the team |

If it would help another marketer, it belongs in the repo.

## Step 3: Make The Changes

1. Read target files before editing.
2. Add concise, practical context in the file's existing structure.
3. If editing a system doc, update `<!-- last-reviewed: YYYY-MM-DD -->`.
4. If the learning is substantial, create a PR. If it is a tiny stale-link or typo fix, make the edit directly.

## Step 4: Confirm

Show what was captured and where:

```markdown
Captured learnings:

1. Added CRM re-enrollment caveat to systems/owned/crm-lifecycle.md
2. Updated campaign launch checklist with the tracking QA step
3. Fixed stale #campaign-launches channel ID in references/slack.md

These changes are [committed / ready for PR].
```

## When To Suggest This Skill

Suggest `/retro` after work where:

- The user had to explain a step that is not documented
- A platform behaved in a surprising way
- A campaign or channel result changed the team's playbook
- A skill routed incorrectly or lacked a fallback
- A partner approval or handoff rule became clear

Use this prompt:

> We learned something useful here. Want to run `/retro` so the next campaign benefits from it?

## Key Principles

- **Repo over memory.** Team knowledge belongs in version-controlled files.
- **Small and immediate beats big and late.** Capture the useful part while it is fresh.
- **Avoid duplicates.** Update the source section instead of creating a second copy.
- **Keep it actionable.** Write what a marketer should do differently next time.
