# {{TEAM_NAME}} - Marketing Brain

> {{TEAM_NAME}}'s operating brain for campaigns, channels, marketing systems, partner handoffs, and measurement. Structured for Claude, maintained by the team.

## Quick Start

Open Claude Code in this repo and say any of these:

| Say this | What happens |
|----------|--------------|
| "good morning" | Daily marketing brief with active work, blockers, Slack highlights, and next moves |
| "run the marketing OS" | Triage or plan broad marketing work across systems and channels |
| "create a task" | Campaign-ready monday task with Why, Audience, Message, Channel, and Done When |
| "interview me" | Claude extracts marketing tribal knowledge and updates the repo |
| "let's retro" | Captures campaign or workflow learnings for next time |
| "health check" | Finds stale docs, missing references, and routing gaps |
| "what skills do you have?" | Lists available Marketing Brain workflows |

## Skills

| Skill | Trigger phrases | Description |
|-------|-----------------|-------------|
| `marketing-os` | "run the marketing OS", "triage marketing", "plan this campaign" | Top-level router for broad campaign, channel, planning, and performance work |
| `good-morning` | "good morning", "morning brief", "catch me up" | Daily brief with active marketing work, blockers, Slack highlights, and actions |
| `pm-story` | "create a task", "write this up", "turn this into a brief" | Structured monday task creation grounded in marketing context |
| `retro` | "let's retro", "capture what we learned" | Captures launch, campaign, and workflow learnings in the repo |
| `health-check` | "health check", "stale docs" | Checks freshness, placeholders, references, and skill routing |
| `curious-intern` | "interview me", "fill gaps", "brain dump" | Interview flow for extracting marketing tribal knowledge |
| `team-intro` | "tell me about the team", "onboard me" | Marketing team, systems, channels, and workflow overview |
| `list-skills` | "what skills do you have", "list skills" | Shows all available skills from the repo |
<!-- Add custom skills here as you create them -->

## Systems We Own

| System | Doc |
|--------|-----|
<!-- Systems are populated during setup and as you document more -->

See `systems/README.md` for templates. Say "teach me about [system name]" to fill in a real system doc.

## Team

**{{TEAM_NAME}}** - `#{{TEAM_SLACK_CHANNEL}}`

See `references/team.md` for the roster and focus areas.

## How This Repo Works

```text
CLAUDE.md (always loaded - the operating map)
  |
  +-- references/      (people, channels, boards, partner teams)
  +-- systems/         (marketing platforms, workflows, dependencies)
  +-- .claude/skills/  (repeatable workflows triggered by natural language)
```

Claude loads only the context needed for the current task. Details in `PHILOSOPHY.md`.

## Adding To This Repo

- **New skill:** say "I want to create a skill for [workflow]"
- **New system doc:** say "teach me about [system name]"
- **Campaign learning:** say "let's retro" after launches, tests, reporting cycles, or messy workflows
- **Health check:** say "health check" monthly or after major team/system changes

## Adoption Guide

See `docs/QUICKSTART.md` for the full playbook: first 30 minutes, first week, first month, decision trees, migration guidance, and common pitfalls.

<details>
<summary>Git hooks setup</summary>

This repo includes a pre-commit hook for secret scanning:

```bash
git config core.hooksPath .githooks
```

The hook runs automatically if configured. If `gitleaks` is unavailable, it falls back to a basic pattern check.

</details>
