# Marketing Brain Philosophy

Guidelines for building and maintaining a marketing operating brain that Claude can use without turning every request into a fresh discovery call.

## Principles

### 1. Link to Sources, Do Not Copy Them

Never copy live campaign data, customer lists, dashboard screenshots, API responses, ad account exports, or CRM records into this repo. Use pointers: board URLs, dashboard links, CRM views, CMS paths, asset folders, Slack channel IDs, and owner names.

This keeps the brain useful without making it stale:

- Claude can fetch or ask for the current source of truth.
- The repo does not drift when a campaign, metric, or asset changes.
- Sensitive or fast-changing marketing data stays in the platform that owns it.

### 2. Let the AI Interview the Marketer

Do not try to write perfect marketing documentation from a blank page. Instead:

- Tell Claude which campaign, channel, platform, or workflow you want it to learn.
- Let it ask you targeted questions.
- Review the result and correct the nuance.
- Commit the useful context so the next teammate gets the benefit.

The interview method captures the practical layer marketers actually need: what matters, who approves, what usually breaks, and how success is judged.

### 3. Make Every Campaign Teach the Next One

At the end of a launch, messy triage, reporting cycle, or new workflow, run `/retro`. Capture the audience insight, channel gotcha, approval rule, measurement caveat, or handoff step while it is still fresh.

If the learning stays in one person's chat history, the team loses it. If it lands in the repo, the next campaign starts smarter.

### 4. Treat Claude as a Marketing Ops Interface

Every time you click through the same web interface - monday boards, CRM workflows, CMS pages, ad account settings, analytics dashboards, Slack approvals - ask: "Can this become a skill?"

A good skill turns a repeated workflow into a consistent operating path with fewer dropped steps and better handoffs.

### 5. Keep the Brain Clean

A messy Marketing Brain causes confident wrong answers. Maintenance rules:

- **Review:** Re-read high-impact system docs on a regular cadence.
- **Audit:** Check skill triggers, board IDs, channel IDs, and owner paths.
- **Learn:** Capture workflow and campaign learnings with `/retro`.
- **Prune:** Remove dead skills, stale examples, and unused placeholders.
- **Handoff:** When ownership changes, move the context into the repo before it disappears.

Run `/health-check` periodically to find stale docs, unfilled placeholders, and routing gaps.

## Anti-Patterns

| Do not | Why it hurts | Do instead |
|--------|--------------|------------|
| Write huge docs before doing real work | No immediate value, gets stale quickly | Build through live workflows and retros |
| Copy dashboard numbers or CRM exports | Creates stale or sensitive copies | Link to the dashboard, report, list, or board |
| Save marketing system knowledge to memory | Only one user benefits and nobody can review it | Commit durable knowledge to the repo |
| Let old skills linger | Stale skills route work incorrectly | Run `/health-check` and prune quarterly |
| Skip launch retros | Campaign learning stays tribal | Capture what changed, what worked, and what broke |
| Overload `CLAUDE.md` | Claude reads it every time | Put detail in system docs, references, and skills |

## How Agents Navigate This Repo Efficiently

The repo works through **progressive disclosure**: give Claude a map first, then let it load the right operating context.

```text
1. CLAUDE.md (always loaded)
   - Explains the marketing team, routing, and operating rules
   - Points to where stable context lives

2. Targeted files (loaded on demand)
   - "Check lifecycle nurture performance" -> read the CRM/lifecycle system doc
   - "Create a task" -> trigger pm-story and read monday board references

3. Deep knowledge (loaded within skills)
   - A skill may load campaign checklists, query patterns, or platform-specific notes
   - Heavy context is loaded only when the workflow needs it
```

The result: Claude gets enough context to act well without dragging every campaign, channel, and dashboard into every conversation.

## What Belongs Where

| Content type | Location | Example |
|--------------|----------|---------|
| Team identity and routing rules | `CLAUDE.md` | Primary Slack channel, morning brief sources, skill registry |
| Marketing platforms and workflows | `systems/owned/*.md` | CRM lifecycle, website CMS, paid acquisition, campaign calendar |
| Partner-owned dependencies | `systems/reference/*.md` | Product analytics, brand library, data warehouse, sales CRM |
| Stable lookup data | `references/*.md` | Slack channel IDs, monday column keys, partner contacts |
| Repeatable workflows | `.claude/skills/*/SKILL.md` | Launch brief, campaign retro, content refresh, reporting readout |
| Heavy reference within a skill | `.claude/skills/*/knowledge/*.md` | Query patterns, checklist details, platform caveats |
| Code-level conventions | That code repo's `CLAUDE.md` | Frontend patterns, API conventions, deployment rules |
| One person's preferences | Memory | "Use concise bullets in my Slack drafts" |
