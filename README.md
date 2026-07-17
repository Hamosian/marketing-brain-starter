# Marketing Brain Starter

> A ready-to-fork operating kit for marketing teams that want Claude to understand their campaigns, channels, audiences, systems, boards, and launch rhythms from day one.

## What This Is

Marketing work moves across a lot of surfaces: campaign boards, Notion databases, ClickUp lists, CRM workflows, landing pages, ad accounts, analytics dashboards, Slack threads, launch calendars, and partner teams. Without a shared context layer, every AI conversation starts from scratch.

This starter gives your team a **Marketing Brain**: a version-controlled knowledge base and skill set that Claude can load progressively as it helps plan, triage, execute, measure, and learn from marketing work.

```text
CLAUDE.md (always loaded - the operating map)
  |
  +-- marketing-os     (top-level router for broad marketing work)
  +-- references/      (stable lookup data: people, channels, boards, partners)
  +-- systems/         (maps of marketing platforms, workflows, and dependencies)
  +-- .claude/skills/  (repeatable workflows triggered by natural language)
```

Claude loads only the context needed for the current request. Campaign learnings, workflow fixes, and platform gotchas go back into the repo, so the team gets smarter every time the work runs.

## Quick Start

1. **Fork or copy this repo** into a repository your marketing team owns.
2. **Open Claude Code in the repo** and say: **"set up my marketing brain"**.
3. Answer the setup questions for your team, Slack channel, work tracker, owned marketing systems, and partner teams. The starter is wired for monday.com by default; Notion and ClickUp work as alternatives once you adapt the tracker references and skills.
4. Say **"good morning"** for your first daily marketing brief, or **"run the marketing OS"** to triage a broader request.

## What's Inside

| Skill | Say something like... | What it does |
|-------|-----------------------|--------------|
| `setup` | "set up my marketing brain" | One-time onboarding wizard that turns placeholders into your real marketing operating context |
| `marketing-os` | "run the marketing OS" | Routes broad marketing requests across campaign, content, CRM, web, paid, lifecycle, and measurement work |
| `daily-brief` | "good morning", "morning brief" | Daily brief with active marketing work, open blockers, Slack highlights, and recommended actions |
| `marketing-brief` | "create a task", "write this up" | Turns a request into a campaign-ready tracker brief with Why, Audience, Message, Channel, and Done When |
| `retro` | "let's retro" | Captures campaign and workflow learnings so the next launch starts ahead |
| `health-check` | "health check", "stale docs" | Finds stale system docs, missing references, and routing gaps |
| `knowledge-interview` | "interview me", "fill gaps" | Interviews the team to extract marketing tribal knowledge into durable docs |
| `team-intro` | "tell me about the team", "onboard me" | Gives new teammates a map of the team, systems, channels, and workflows |
| `list-skills` | "what skills do you have?" | Lists every available skill, read live from the repo |

Plus:

- **`references/`** - team roster, Slack channels, tracker boards/databases/lists, partner teams, and stable IDs
- **`systems/`** - templates and examples for CRM, lifecycle, website, paid, content, events, analytics, and partner-owned dependencies
- **Marketing Brain lint** (`.github/workflows/team-context-lint.yml`) - keeps skills well-formed and placeholder cleanup visible
- **Pre-commit secret scanning** (`.githooks/pre-commit`) - helps keep tokens and credentials out of the repo

## How It Grows

The starter is intentionally small. The intended path:

1. **Week 1:** run `/setup`, document your 2-3 highest-leverage marketing systems, and use `/daily-brief` daily.
2. **As you work:** end new or messy workflows with `/retro` so launch notes, channel learnings, and workflow fixes land in the repo.
3. **As you scale:** add specialist skills for CRM, lifecycle, paid acquisition, website, SEO, content, events, partner marketing, or measurement, then register them in `CLAUDE.md`.

`docs/QUICKSTART.md` has the full adoption playbook: first 30 minutes, first week, first month, decision trees, migration guidance, and common pitfalls.

## Principles

- **Marketing context, not generic documentation** - capture the audience, channel, offer, metric, owner, and decision path.
- **Pointers, not copies** - link to live boards, dashboards, CRM views, CMS pages, and campaign assets instead of duplicating data.
- **Repo over memory** - durable team knowledge belongs in reviewed files where the whole marketing org can benefit.
- **Every campaign teaches the next one** - retros turn one-off launch learning into reusable operating advantage.

## Requirements

- [Claude Code](https://claude.com/claude-code) (CLI, desktop, or web)
- Work tracking in monday.com by default, or Notion/ClickUp if you adapt the tracker references and skills
- Slack for team and partner communication
- Optional integrations as your team needs them: CRM, analytics, ad platforms, CMS, GitHub, Google Drive, Graphify, or other marketing systems

## Optional Add-On: Graphify

[Graphify](https://github.com/Graphify-Labs/graphify) can turn this repo, docs, schemas, and media into a queryable knowledge graph when your team wants a visual map of how the Marketing Brain fits together.

Install the CLI once:

```bash
uv tool install graphifyy
```

Then install the project skill for the assistant your team uses:

```bash
# Codex
graphify install --project --platform codex

# Claude Code
graphify install --project
```

After installing it for the project, run `$graphify .` in Codex or `/graphify .` in Claude Code. Generated files go into `graphify-out/` and `graph.json`, which are ignored by git and Claude context.

## License

MIT - see `LICENSE`. Use it, fork it, make it your team's marketing brain.
