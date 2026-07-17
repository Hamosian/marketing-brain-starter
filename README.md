# Marketing Brain Starter

> A free, ready-to-fork template for building your marketing team's **AI operating brain**: a version-controlled knowledge base that turns Claude from a blank-slate assistant into an operating partner that knows your systems, boards, channels, and workflows.

## What This Is

Most teams use AI as an isolated tool: every session starts from zero, knowledge lives in one person's chat history, and nothing compounds. This starter flips that. It gives you a **context repo** - a structured, git-versioned brain that Claude loads progressively:

```
CLAUDE.md (always loaded - the map)
  |
  +-- marketing-os    (top-level router for broad/cross-system work)
  +-- references/     (stable lookup data: IDs, contacts, boards)
  +-- systems/        (architecture maps of what you own)
  +-- .claude/skills/ (automated workflows triggered by natural language)
```

Claude loads only what the current task needs. Every learning goes back into the repo as a pull request, so the brain gets smarter with every workflow. See `PHILOSOPHY.md` for why this works and the flywheel that keeps it healthy.

This template ships marketing-flavored, but the structure works for any team - the setup wizard supports engineering, data, sales, HR, and finance flavors too.

## Quick Start

1. **Use this template** (or fork/clone it) into a repo your team owns.
2. **Open Claude Code in the repo** and say: **"set up my team context"**.
3. Answer the wizard's questions (team name, Slack channel, Monday board...). It replaces every curly-brace `{{...}}` marker in the repo with your real data - takes about 5 minutes.
4. Say **"good morning"** for your first daily brief.

## What's Inside

| Skill | Say something like... | What it does |
|-------|-----------------------|--------------|
| `setup` | "set up my team context" | One-time onboarding wizard - fills in all placeholders |
| `marketing-os` | "run the marketing OS" | Top-level router: triages broad requests, delegates to sub-agents, closes the loop |
| `good-morning` | "good morning", "morning brief" | Daily brief: active tasks, unowned bugs, Slack highlights, suggested actions |
| `pm-story` | "create a task", "write a story" | Structured Monday task creation (Why / What / Done When), grounded in system context |
| `retro` | "let's retro" | Captures learnings after any workflow and commits them to the repo |
| `health-check` | "health check", "stale docs" | Finds stale docs, template drift, and knowledge gaps |
| `curious-intern` | "interview me", "fill gaps" | Interviews you to systematically extract tribal knowledge into docs |
| `team-intro` | "tell me about the team", "onboard me" | Team and systems overview for new joiners |
| `list-skills` | "what skills do you have?" | Lists every available skill, read live from the repo |

Plus:

- **`references/`** - templates for your team roster, Slack channels, Monday boards, and cross-team contacts
- **`systems/`** - doc templates (full + light) and worked examples for mapping the systems you own
- **CI lint** (`.github/workflows/team-context-lint.yml`) - keeps skills well-formed, placeholders filled, and binaries out
- **Pre-commit secret scanning** (`.githooks/pre-commit`) - gitleaks with a grep fallback; enable with `git config core.hooksPath .githooks`

## How It Grows

The starter is deliberately small. The intended path:

1. **Week 1:** run `/setup`, document your 2-3 most important systems ("teach me about our CRM"), run `/good-morning` daily.
2. **As you work:** end novel workflows with `/retro` - learnings land as PRs, never as tribal memory.
3. **As you scale:** build domain sub-agents (data, CRM, paid, website, SEO, content, campaigns...) and register them in `CLAUDE.md`'s Sub-Agent Registry. `marketing-os` routes to whatever the registry contains.

`docs/QUICKSTART.md` has the full adoption playbook: first 30 minutes, first week, first month, decision trees, and common pitfalls.

## Principles

- **Progressive disclosure** - CLAUDE.md is a map, not an encyclopedia. Details load on demand.
- **Pointers, not copies** - link to dashboards and boards; never duplicate live data into the repo.
- **Repo over memory** - team knowledge belongs in reviewed PRs where everyone benefits, not in one person's AI memory.
- **Every workflow teaches the next one** - the retro loop is the whole point.

## Requirements

- [Claude Code](https://claude.com/claude-code) (CLI, desktop, or web)
- Optional integrations, connected as you go: monday.com (MCP, OAuth), Slack, your CRM, GitHub

## License

MIT - see `LICENSE`. Use it, fork it, share it.
