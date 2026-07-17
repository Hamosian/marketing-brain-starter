# {{TEAM_NAME}} - Marketing Brain

## Purpose

This repo is {{TEAM_NAME}}'s **Marketing Brain**: a version-controlled operating layer for campaign planning, channel execution, lifecycle workflows, partner handoffs, and measurement. It gives Claude the durable context needed to act like a marketing operations partner instead of a blank-slate assistant.

Everything here is structured for **progressive disclosure**. Claude starts with this file, then loads only the references, system docs, or skills needed for the current request.

For the operating philosophy behind this repo - why it is built this way and how the learning loop compounds - see `PHILOSOPHY.md`.

> **First time here?** If this file still contains unfilled curly-brace `{{...}}` markers, run `/setup` or say "set up my marketing brain".

## How This Repo Works

```text
CLAUDE.md (always loaded)
  |
  +-- marketing-os     (top-level router for broad marketing work)
  +-- references/      (on demand - people, channels, boards, partner teams)
  +-- systems/         (on demand - marketing platforms, workflows, dependencies)
  +-- .claude/skills/  (on trigger - repeatable marketing workflows)
       +-- knowledge/  (on demand within skills - heavier source material)
```

**Rule:** Load the relevant context as soon as a task points to it. Do not preload every file at session start.

## Reference Files

| File | Contains |
|------|----------|
| `references/team.md` | Marketing team roster, focus areas, Slack IDs, and emails |
| `references/other_teams.md` | Product, Sales, Data, Design, Web, and other partner teams |
| `references/slack.md` | Channel IDs, announcement channels, intake channels, and user groups |
| `references/monday_boards.md` | Work tracker IDs and fields: monday boards by default, or equivalent Notion databases / ClickUp lists |

## Systems Reference

Load the relevant file when a task mentions a platform, channel, workflow, or measurement surface.

**Owned marketing systems:**

| System | File |
|--------|------|
<!-- Populated during /setup and as you document more systems. Examples: -->
<!-- | CRM and Lifecycle | `systems/owned/crm-lifecycle.md` | -->
<!-- | Marketing Website | `systems/owned/marketing-website.md` | -->
<!-- | Paid Acquisition | `systems/owned/paid-acquisition.md` | -->
<!-- | Campaign Calendar | `systems/owned/campaign-calendar.md` | -->

**Reference systems (important, but owned elsewhere):**

| System | File |
|--------|------|
<!-- Example: | Product Analytics (owned by Data) | `systems/reference/product-analytics.md` | -->
<!-- Example: | Brand Asset Library (owned by Design) | `systems/reference/brand-library.md` | -->

## Knowledge Routing

When something useful is learned during marketing work, route it to the right place:

| What was learned | Where it goes | How |
|-----------------|---------------|-----|
| Platform behavior, workflow quirk, campaign risk, or failure mode | `systems/owned/<system>.md` | Edit the system doc and open a PR |
| Repeatable launch, channel, CRM, content, or reporting workflow | `.claude/skills/<name>/SKILL.md` or skill `knowledge/` | Update or create the skill |
| Team convention, approval rule, partner handoff, or routing rule | `CLAUDE.md` or `references/` | Add the durable rule |
| Live metric, campaign status, or audience count | Source system only | Link to the dashboard or board, do not copy |
| Personal style preference | Memory | Save only if it applies to one user, not the team |

**Never save marketing system or team operating knowledge to memory.** Anything that helps the team run campaigns, understand channels, move work, or measure impact belongs in this repo where everyone can review and reuse it.

After a new workflow, unexpected blocker, or campaign learning, suggest `/retro` so the learning becomes durable.

## Content Boundary

If the content changes every time a platform refreshes, it belongs in that platform. If it helps Claude understand how marketing work should run across tools, it belongs here.

- **Pointers, not copies** - link to dashboards, monday boards, Notion databases, ClickUp lists, CRM lists, ad accounts, CMS pages, briefs, and asset folders.
- **Progressive disclosure** - put IDs, views, URLs, account names, and platform details in `systems/`, `references/`, or skill `knowledge/` files.
- **Marketing decision context** - capture audience, offer, channel, owner, success metric, approval path, and launch date whenever they matter.

## Editing This Repo

Edits to `CLAUDE.md`, `systems/**`, `references/**`, and `.claude/skills/**` are linted on every PR (`.github/workflows/team-context-lint.yml`). Before opening a PR:

- Every `.claude/skills/*/SKILL.md` starts with YAML frontmatter containing `name:` and `description:`.
- No unfilled setup placeholders remain after setup.
- No binary exports or packaged files live in the repo root. Link to source assets instead.

## Team

- **Team:** {{TEAM_NAME}}
- **Marketing function:** {{TEAM_TYPE}}
- **Group:** {{GROUP_NAME}}
- **Lead:** {{TEAM_LEAD_NAME}}
- **Manager:** {{MANAGER_NAME}}
- **Marketing stack:** {{TECH_STACK}}
- **Work tracker:** monday.com by default (`{{MONDAY_WORKSPACE}}.monday.com`), or Notion/ClickUp if adapted
- **Primary Slack:** `#{{TEAM_SLACK_CHANNEL}}` (channel ID: `{{TEAM_SLACK_CHANNEL_ID}}`)
- **Primary tracker board/list/database:** Tasks `{{MONDAY_TASKS_BOARD_ID}}` (full details in `references/monday_boards.md` or the adapted tracker reference)

Full roster, Slack IDs, emails, and focus areas live in `references/team.md`.

## Task Routing

Different marketing requests use different entry points. If a skill exists for the work, use it.

| Task type | Start with |
|-----------|------------|
| Broad or cross-channel marketing work | `/marketing-os` - routes, prioritizes, synthesizes, and closes the loop |
| Campaign, content, CRM, or ops task creation | `/pm-story` - writes the full tracker brief |
| Daily work and risk scan | `/good-morning` |
| Capturing campaign or workflow learnings | `/retro` |
| Checking repo health | `/health-check` |
| Extracting tribal knowledge | `/curious-intern` |
| Team overview and onboarding | `/team-intro` |
| Listing available skills | `/list-skills` |
<!-- Add rows as the team creates specialist skills. Examples: -->
<!-- | Brand and messaging | `/brand-guidelines` - voice, positioning, visual rules | -->
<!-- | Landing page CRO | `/page-cro` - audit and optimize conversion surfaces | -->
<!-- | Lifecycle programs | `/lifecycle-agent` - email, nurture, segmentation, automation | -->
<!-- | Campaign launch | `/campaign-launch` - brief, checklist, owners, measurement | -->

## Sub-Agent Registry

For broad requests, start with `/marketing-os`; it chooses from this registry and synthesizes the final recommendation.

| Domain | Skill |
|--------|-------|
| Work intake and task briefs | `/pm-story` |
| Learning and repo hygiene | `/retro`, `/curious-intern`, `/health-check` |
<!-- Grow this registry as you build domain sub-agents. Examples: -->
<!-- | Measurement and reporting | `/measurement-agent`, `/analytics-agent` | -->
<!-- | CRM and lifecycle | `/crm-agent`, `/lifecycle-agent` | -->
<!-- | Content and messaging | `/content-agent`, `/brand-guidelines` | -->
<!-- | Paid acquisition | `/paid-acquisition-agent` | -->
<!-- | Website and CRO | `/website-agent`, `/page-cro` | -->
<!-- | SEO and AI search | `/seo-agent` | -->
<!-- | Campaign orchestration | `/campaign-agent` | -->
<!-- | Events and webinars | `/events-agent` | -->

**Catch-all:** `/marketing-os` may invoke any skill in `.claude/skills/` when it fits the task, even if the skill is not listed here. When unsure, consult `/list-skills`.

## Morning Brief Sources

The `/good-morning` skill reads this table to decide what to include in the daily brief. Uncomment sources your team uses.

| Source | Type | Config | Enabled |
|--------|------|--------|---------|
| Active marketing work | tracker | monday board / Notion database / ClickUp list: `{{MONDAY_TASKS_BOARD_ID}}` | Yes |
| Unowned requests or blockers | tracker | owner empty or blocked in the configured tracker | Yes |
| Slack: team channel | slack | channel: `{{TEAM_SLACK_CHANNEL_ID}}` (#{{TEAM_SLACK_CHANNEL}}) | Yes |
<!-- | Campaign calendar | tracker | monday board / Notion database / ClickUp list: your-campaign-calendar | No | -->
<!-- | Website launches | tracker | monday board / Notion database / ClickUp list: your-website-work | No | -->
<!-- | Open PRs | github | repos: your-org/your-repo | No | -->
<!-- | Merged PRs | github | repos: your-org/your-repo | No | -->

## Global Agent Directives

- **Marketing OS first:** If a request spans channels, platforms, audiences, launch timing, prioritization, or unclear marketing intent, use `/marketing-os`.
- **Evidence beats vibes:** Name the source and limitation behind performance claims, audience claims, or prioritization recommendations.
- **Load context proactively:** When a request mentions a system, channel, campaign, or platform, load its system doc before acting.
- **Approval before writes:** Ask before mutating CRM records, monday items, Notion pages/databases, ClickUp tasks, ad platforms, CMS pages, Slack messages, email tools, or production workflows unless a specific automation explicitly allows it.
- **Campaign-ready output:** For briefs and tasks, capture why it matters, audience, message/offer, channel/surface, owner, due date, and Done When.
- **Slack tone:** Messages sent for the team should be warm, clear, and human. Reply in-thread when the context is a thread.
- **Slack attribution:** Every Slack message sent by an agent ends with `_Posted by the team's AI agent_`.
- **Task creation:** Use `/pm-story` for task creation so the tracker gets a complete marketing brief instead of a bare title.
- **Self-improvement:** When a workflow produces a non-obvious learning, suggest `/retro`.
- **Partner context:** If a task involves another team, check `references/other_teams.md` for contact, channel, intake path, and context repo.
