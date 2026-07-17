# Marketing Brain Quickstart

## Prerequisites

Before you start, make sure you have:

- [ ] **Claude Code** installed and working
- [ ] A **work tracker**: monday.com workspace, Notion database, or ClickUp space/list for marketing work and campaign planning
- [ ] A **Slack channel** for your marketing team
- [ ] At least **one marketing system** worth documenting: CRM, lifecycle, CMS, website, paid acquisition, content calendar, events, reporting, or campaign operations
- [ ] A **team champion** who will use the brain publicly for the first two weeks

## Quickstart (3 Steps)

### 1. Create a new repo on GitHub

Use a repo your marketing team owns. Good names: `{team-slug}-marketing-brain`, `{team-slug}-campaign-brain`, or `{team-slug}-gtm-brain`.

### 2. Pull in the starter

```bash
cd your-repo
npx degit Hamosian/marketing-brain-starter . && git add -A && git commit -m "init: marketing brain starter"
```

This copies the starter files into your repo without preserving the starter's git history.

### 3. Open Claude Code and say: "set up my marketing brain"

The `/setup` skill will ask about your marketing team, primary Slack channel, work tracker, owned marketing systems, and partner teams. The starter ships with monday.com wiring by default; if your team uses Notion or ClickUp, document equivalent database/list IDs and adapt tracker-specific skills as needed.

After setup, try:

- "good morning" for a daily marketing brief
- "run the marketing OS" for campaign triage or planning
- "teach me about our CRM" to document your first system

## Optional: Add Graphify

If your team wants a visual, queryable map of the repo, [Graphify](https://github.com/Graphify-Labs/graphify) can scan the Marketing Brain and generate a knowledge graph.

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

Then run `$graphify .` in Codex or `/graphify .` in Claude Code. Graphify output is ignored at `graphify-out/` and `graph.json` so generated artifacts stay uncommitted.

## First 30 Minutes

### Confirm the skills loaded (5 min)

Say "what skills do you have?" You should see: marketing-os, daily-brief, marketing-brief, retro, health-check, knowledge-interview, team-intro, and list-skills.

### Document the first marketing system (20 min)

Pick the system that most often slows people down. Good first choices:

- CRM and lifecycle automation
- Marketing website or CMS
- Paid acquisition accounts
- Campaign calendar and launch process
- Reporting and attribution dashboards

Tell Claude:

> "I want to teach you about [System Name]"

Let Claude interview you. It should capture what the system does, who owns it, where the live source lives, what usually breaks, how marketers use it, and how success is measured.

**Do not write the system doc from scratch.** The interview approach produces better AI-ready context because it pulls out routing rules, platform caveats, and practical handoff details.

### Try the morning brief (5 min)

Say "good morning." Claude will read the configured work tracker and Slack channel, then summarize active work, open blockers, Slack highlights, and suggested next actions.

If the brief feels noisy, tighten `references/monday_boards.md`: document which monday groups, Notion database views, or ClickUp lists count as active, which statuses are parked, and which fields matter.

## First Week

### Day 2-3: Add your core systems

Document 2-3 more owned systems using the interview approach. Each should take 15-20 minutes.

Strong marketing starter set:

- CRM and lifecycle
- Website and CMS
- Paid acquisition
- Campaign calendar
- Content operations
- Measurement and reporting

Check `systems/examples/` for marketing-native examples.

### Day 3-4: Create your first custom skill

Choose a workflow the team repeats often:

- Launching a campaign
- Writing a campaign brief
- Reviewing content performance
- Auditing CRM automation
- Preparing a weekly marketing readout
- QAing a landing page before launch
- Turning Slack feedback into board tasks

Tell Claude: "I want to create a skill for [workflow]." Use the `/skill-creator` plugin if available.

### Day 5: Team demo

Show the team three things:

1. A real "good morning" brief
2. A campaign/task brief created with `/marketing-brief`
3. A system doc Claude uses during a workflow

This is the adoption moment. Marketers believe the brain when it helps with work they already recognize.

## First Month

### Week 2: Add specialist workflows

Build 2-3 skills around live marketing work. Broad requests should start in `/marketing-os`, then delegate to specialist skills as they appear.

Good candidates:

- Campaign launch checklist
- Weekly performance readout
- Lifecycle nurture QA
- Paid experiment intake
- Website CRO audit
- Content refresh workflow

End new workflows with `/retro` so learnings become reusable.

### Week 3: Fill reference data

Complete:

- Work tracker field names and status values (`references/monday_boards.md` for monday, or equivalent Notion/ClickUp reference notes)
- Partner team contacts (`references/other_teams.md`)
- Slack channels and user groups (`references/slack.md`)
- Team roster and focus areas (`references/team.md`)

### Week 4: Health check and retro

Run `/health-check` to find stale docs, missing owners, and routing gaps. Run `/knowledge-interview` to extract the knowledge that still lives in people's heads.

## Decision Trees

### "Where does this knowledge go?"

```text
Is it about how a MARKETING SYSTEM works?
  -> systems/owned/<system>.md or systems/reference/<system>.md

Is it a REPEATABLE WORKFLOW?
  -> .claude/skills/<workflow>/SKILL.md

Is it STABLE LOOKUP DATA?
  -> references/<topic>.md

Is it a TEAM ROUTING RULE or MARKETING OPERATING CONVENTION?
  -> CLAUDE.md

Is it LIVE PERFORMANCE DATA or CURRENT CAMPAIGN STATUS?
  -> Keep it in the source platform; add only a pointer here

Is it one person's style preference?
  -> Memory
```

### "Should this be a skill or a system doc section?"

```text
Can Claude run or guide the workflow step by step?
  -> Skill

Does Claude need it to understand a platform, channel, or dependency?
  -> System doc

Does it involve judgment at every step?
  -> System doc plus a guided skill if the team repeats it

Does it cross several marketing systems?
  -> Start with marketing-os, then create specialist skills over time
```

## Common Pitfalls

| Pitfall | Why it hurts | Prevention |
|---------|--------------|------------|
| Writing a huge marketing wiki upfront | It delays value and goes stale | Start with live workflows, then capture learnings |
| Copying live metrics into docs | Numbers go stale immediately | Link to dashboards and explain how to read them |
| Leaving tracker fields undocumented | Skills cannot set reliable metadata | Fill exact field keys, labels, and statuses in `references/monday_boards.md` or the equivalent Notion/ClickUp reference |
| Skipping `/retro` after launches | Campaign learning disappears | Make retro part of the launch closeout |
| One person maintaining the brain | Creates bottlenecks | Rotate a "marketing brain gardener" weekly |
| Overloading `CLAUDE.md` | Slows every task | Move detail into system docs and skills |
| Keeping stale examples | Claude routes work through fake context | Delete examples once real system docs exist |

## The Adoption Demo

When introducing the Marketing Brain:

1. **Show the work first.** Do not start with repo philosophy.
2. **Run a brief:** say "good morning" and show the operating readout.
3. **Create a task:** pick a real request and run `/marketing-brief`.
4. **Use context:** ask about a system and show Claude reading the relevant doc.
5. **Then explain the loop:** every useful learning gets captured back into the repo.
6. **Assign ownership:** each marketer documents one system, channel, or repeated workflow in the first week.

## Migration Guide: Existing Documentation

If your team already has docs in Notion, Google Docs, Confluence, Drive, or wikis:

### What to migrate

- Platform maps -> `systems/owned/<system>.md`
- Launch checklists and playbooks -> `.claude/skills/<workflow>/SKILL.md`
- Team roster and focus areas -> `references/team.md`
- Board, channel, view, and report IDs -> `references/`
- Partner handoffs -> `references/other_teams.md`

### What not to migrate

- Meeting notes
- Screenshots of dashboards or CRM records
- Old campaign readouts with no reusable learning
- Full brand or product docs owned elsewhere
- Anything that duplicates a live source of truth

### How to migrate

Do not copy-paste whole docs. Instead:

1. Open the old doc and the relevant template.
2. Tell Claude: "I'm migrating our [workflow/system] docs. Here are the useful points."
3. Let Claude interview you to fill the missing operational context.
4. Review the result for accuracy, then commit it.

## Creating Your First Custom Skill

### When to create a skill

If you have guided Claude through the same marketing workflow more than twice, create a skill. Signs:

- You keep pasting the same launch checklist.
- You keep explaining the same board IDs, channel rules, or approval path.
- The workflow has a predictable sequence and common failure cases.

### How to create one

1. Tell Claude: "I want to create a skill for [workflow]."
2. Capture:
   - YAML frontmatter with a clear `name` and trigger-rich `description`
   - Step-by-step workflow instructions
   - Source systems and references to load
   - Approval rules for writes
   - Fallbacks for platform errors
3. Save it to `.claude/skills/<name>/SKILL.md`.
4. Add it to the skill table in `README.md` and the registry in `CLAUDE.md` if it is a domain sub-agent.
5. Test it with 3-5 natural trigger phrases.

### Skill format

```markdown
---
name: skill-name
description: Use this skill when the user wants to run [marketing workflow]. Triggered by "natural phrase", "another phrase".
---

# Skill Title

Step-by-step instructions for Claude to follow.
```

### Tips

- Keep `SKILL.md` under 500 lines. Put heavy reference material in `knowledge/`.
- Write in imperative voice: "Read...", "Check...", "Ask...", "Draft...".
- Explain why a step matters when the marketing judgment is not obvious.
- Include approval rules before sending messages, changing CRM data, or updating live platforms.
- Include fallback guidance for common platform errors.

## Maintenance

### The Review Loop

Review the Marketing Brain quarterly:

- **Review:** Does each skill still match the way the team works?
- **Audit:** Do trigger phrases route to the right skill?
- **Learn:** Did recent launches teach anything not yet captured?
- **Prune:** Remove dead skills, old examples, and obsolete partner paths.
- **Handoff:** Move knowledge from departing owners into the repo.

### Staying Current

- Run `/health-check` monthly.
- Run `/knowledge-interview` after major campaign, platform, or org changes.
- Update `last-reviewed` dates when you verify a system doc.
- Delete example system docs once real docs exist.
