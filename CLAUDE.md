# {{TEAM_NAME}} - Team Context

## Purpose

This repo is {{TEAM_NAME}}'s **Marketing Brain** - a centralized, version-controlled knowledge base designed for AI-first consumption. It transforms Claude from an isolated tool into an operating partner that understands your systems, workflows, conventions, tribal knowledge, and priorities.

Everything here is structured for **progressive disclosure**: Claude loads only what's needed for the current task, not the entire knowledge base. CLAUDE.md (this file) is always loaded. Everything else is loaded on demand.

For the philosophy behind this approach - why it's built this way, the flywheel effect, and the principles that keep it healthy - see `PHILOSOPHY.md`.

> **First time here?** If this file still contains unfilled curly-brace `{{...}}` markers, run `/setup` - the interactive wizard fills everything in from a short interview.

## How This Repo Works

```
CLAUDE.md (always loaded)
  |
  +-- marketing-os     (top-level router for broad/cross-system work)
  +-- references/    (on demand - stable lookup data: IDs, contacts, boards)
  +-- systems/       (on demand - architecture maps of what you own)
  +-- .claude/skills/ (on trigger - sub-agents and workflows)
       +-- knowledge/  (on demand within skills - heavy reference content)
```

**Rule:** Load files proactively when they're relevant to the task at hand - don't wait for the user to ask. But don't preload everything at session start.

## Reference Files

| File | Contains |
|------|----------|
| `references/team.md` | Team roster (single source of truth) - names, Slack IDs, emails |
| `references/other_teams.md` | Other teams you work with - contacts, channels |
| `references/slack.md` | Channel IDs, cross-team channels, user groups |
| `references/monday_boards.md` | Monday board IDs, workspace IDs, column keys |

## Systems Reference

Load the relevant file when working on a system-specific task.

**Owned systems:**

| System | File |
|--------|------|
<!-- Populated during /setup and as you document more systems. Example: -->
<!-- | CRM (HubSpot) | `systems/owned/hubspot.md` | -->
<!-- | Marketing Website | `systems/owned/marketing-website.md` | -->
<!-- | Paid Acquisition | `systems/owned/paid-acquisition.md` | -->

**Reference systems (you depend on, don't own):**

| System | File |
|--------|------|
<!-- Example: | Product analytics (owned by data team) | `systems/reference/product-analytics.md` | -->

## Knowledge Routing

When you learn something new during a task, route it to the right place:

| What you learned | Where it goes | How |
|-----------------|---------------|-----|
| System behavior, platform quirk, failure mode | `systems/owned/<system>.md` | Edit the file, open PR |
| Skill improvement, missing step, wrong assumption | `.claude/skills/<name>/SKILL.md` or `knowledge/` | Edit the file, open PR |
| Team convention, workflow rule | This file (`CLAUDE.md`) or `references/` | Edit the file, open PR |
| User's personal preference or style | Memory | Save to memory |
| Ephemeral task state | Tasks/plans | Use task tools |

**Never save system or team knowledge to memory.** Memory is for individual user preferences only (e.g. "I prefer ASCII diagrams"). Anything about the team, its tools, how systems work, how workflows run, or how this repo operates belongs in the repo where the whole team benefits. If you're unsure, it goes in the repo.

After completing a novel workflow or discovering something non-obvious, suggest running `/retro` to capture the learning properly.

## Content Boundary

If the content would break when the platform it describes changes, it belongs in that platform's source-of-truth. If it's useful regardless of which tool you're in, it belongs here.

- **Pointers, not copies** - link to dashboards, boards, CRM views. Never duplicate live data.
- **Progressive disclosure** - system-specific details (board IDs, dashboard URLs, account IDs) belong in `systems/` or skill `knowledge/` files, not here.

## Editing This Repo

Edits to `CLAUDE.md`, `systems/**`, `references/**`, and `.claude/skills/**` are linted on every PR (`.github/workflows/team-context-lint.yml`). Before opening a PR:
- Every `.claude/skills/*/SKILL.md` must start with YAML frontmatter containing `name:` and `description:`.
- No unfilled template placeholders remain (the curly-brace markers that `/setup` fills in).
- No binary or packaged files (`*.zip`, `*.plugin`, `*.tar.gz`, `*.jar`) in the repo root. Pointers, not copies.

## Team

- **Team:** {{TEAM_NAME}}
- **Team type:** {{TEAM_TYPE}}
- **Group:** {{GROUP_NAME}}
- **Lead:** {{TEAM_LEAD_NAME}}
- **Manager:** {{MANAGER_NAME}}
- **Tools:** {{TECH_STACK}}
- **monday workspace:** `{{MONDAY_WORKSPACE}}.monday.com`
- **Primary Slack:** `#{{TEAM_SLACK_CHANNEL}}` (channel ID: `{{TEAM_SLACK_CHANNEL_ID}}`)
- **Primary Monday boards:** Tasks `{{MONDAY_TASKS_BOARD_ID}}` (full details in `references/monday_boards.md`)

Full roster, Slack IDs, and emails in `references/team.md`.

## Task Routing

Different task types use different entry points. If a skill exists for it, use the skill - it has the full workflow.

| Task type | Start with |
|-----------|-----------|
| Broad or cross-system marketing work | `/marketing-os` - routes to sub-agents, tracks state, closes the loop |
| Task creation | `/pm-story` - writes the full story (Why, What, Done When) |
| Morning brief / standup | `/good-morning` |
| Capturing learnings | `/retro` |
| Checking repo health | `/health-check` |
| Knowledge extraction | `/curious-intern` - interviews you to fill knowledge gaps |
| Team overview / onboarding | `/team-intro` |
| Listing available skills | `/list-skills` |
<!-- Add rows here as you build new skills. Examples from mature instances: -->
<!-- | Brand / visual identity | `/brand-guidelines` - colors, typography, design rules | -->
<!-- | Website page CRO | `/page-cro` - audit and optimize pages for conversion | -->
<!-- | Slide decks | `/branded-presentation` - on-brand .pptx | -->

## Sub-Agent Registry

For broad requests, start with `/marketing-os`; it chooses from this registry and synthesizes the final recommendation.

| Domain | Skill |
|--------|-------|
| Work state and intake | `/pm-story` |
| Learning and repo hygiene | `/retro`, `/curious-intern`, `/health-check` |
<!-- Grow this registry as you build domain sub-agents. Examples from mature instances: -->
<!-- | Data and reporting | `/data-agent`, `/measurement-agent` | -->
<!-- | CRM and lifecycle | `/crm-agent`, `/lifecycle-agent` | -->
<!-- | Comms | `/slack-agent` | -->
<!-- | Brand, content, strategy | `/content-agent` | -->
<!-- | Paid acquisition | `/paid-acquisition-agent` | -->
<!-- | Website and CRO | `/website-agent`, `/page-cro` | -->
<!-- | SEO and AI search | `/seo-agent` | -->
<!-- | Campaign orchestration | `/campaign-agent` | -->

**Catch-all:** `/marketing-os` may invoke any skill in `.claude/skills/` when it fits the task, even if not listed here. When unsure which skill owns a request, consult `/list-skills`.

## Morning Brief Sources

The `/good-morning` skill reads this table to determine what to include in the daily brief. Uncomment sources your team uses.

| Source | Type | Config | Enabled |
|--------|------|--------|---------|
| Active tasks | monday | board: `{{MONDAY_TASKS_BOARD_ID}}` | Yes |
| Unowned bugs | monday | board: `{{MONDAY_TASKS_BOARD_ID}}`, type: bug, unowned | Yes |
| Slack: team channel | slack | channel: `{{TEAM_SLACK_CHANNEL_ID}}` (#{{TEAM_SLACK_CHANNEL}}) | Yes |
<!-- | Open PRs | github | repos: your-org/your-repo | No | -->
<!-- | Merged PRs | github | repos: your-org/your-repo | No | -->

## Global Agent Directives

- **Be concise:** Prefer brief, direct communication. Skip boilerplate explanations.
- **Marketing OS first:** If a request spans multiple systems, starts as vague marketing intent, or needs prioritization, use `/marketing-os` before specialist skills.
- **Load context proactively:** When a task mentions a system, load its system doc without being asked. But don't preload all files at session start.
- **Safety first:** Always ask for confirmation before executing mutating API calls (CRM writes, monday updates, Slack message sending). Unless triggered via a specific automation skill.
- **Slack tone:** Messages sent on behalf of the team should be warm and human - never bare/robotic. If the context is a thread, always reply in the thread (set `thread_ts`).
- **Slack attribution:** Every Slack message must identify that it was sent by an agent. Add a footer line as the last line of the message: `_Posted by the team's AI agent_`.
- **Monday task creation:** Always use the `/pm-story` skill when creating tasks - it handles story writing (Why, What, Done When, Open Questions) on top of item creation. Don't go direct to the API.
- **Self-improvement:** When a workflow produces a non-obvious learning, suggest `/retro` to capture it in the repo. Don't let tribal knowledge stay in one person's memory.
- **Cross-team context:** If a task involves another team's systems, check `references/other_teams.md` for their context repo. Repo naming convention: `{team-slug}-context`.
