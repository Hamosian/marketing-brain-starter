---
name: health-check
description: Use this skill when the user wants to check the health of the Marketing Brain, find stale marketing system docs, missing owners, outdated board or channel references, placeholder residue, or skill routing gaps. Triggered by "health check", "check repo health", "stale docs", "marketing brain health", "are our docs up to date", "what needs updating", "doc hygiene", or "review system docs". Good to run after major launches, org changes, or quarterly planning.
---

# Marketing Brain Health Check

Scan the Marketing Brain for staleness, template drift, broken references, and missing operating context. Report what needs attention so the team can keep the brain trustworthy.

## What To Check

### 1. System Doc Staleness

Read all files in `systems/owned/` and `systems/reference/`. For each file:

1. Look for `<!-- last-reviewed: YYYY-MM-DD -->` on the first line.
2. If missing, flag as **missing review date**.
3. If present, calculate days since last review. Flag as **stale** if older than 90 days.

Present results as a table:

```markdown
| System | Last Reviewed | Status |
|--------|---------------|--------|
| crm-lifecycle.md | 2026-03-31 | OK |
| paid-acquisition.md | 2025-12-15 | STALE |
| campaign-calendar.md | (missing) | NO DATE |
```

### 2. Placeholder And TODO Scan

Search live knowledge files in `systems/owned/`, `systems/reference/`, `references/`, and `CLAUDE.md` for:

- `<!-- TODO` comments
- Empty sections
- Placeholder text such as `TBD`, `TODO`, `FIXME`
- Setup placeholders like `{{TEAM_NAME}}` after setup should have run

Skip `systems/README.md`, `systems/examples/`, and `.claude/skills/setup/`; those intentionally contain templates.

### 3. Template Compliance

For each system doc, determine whether it follows the full or light template:

- Full marketing system docs should include: Overview, How Claude Works With This, Platforms / Data Sources, Operating Model, Key Surfaces, Measurement, Related Systems, Pointers.
- Light partner-owned docs should include: Overview, How Claude Works With This, What Marketing Owns, What Marketing Does Not Own, When It Breaks, Related Systems, Pointers.

Flag missing sections.

### 4. Reference Freshness

Check:

- `references/monday_boards.md` last verified date
- monday board IDs and key columns are documented
- `references/slack.md` has channel IDs for channels used in skills
- `references/other_teams.md` has contact and intake path for partner teams named in system docs
- `references/team.md` has Slack IDs and emails for team members

### 5. Skill Routing Integrity

Check:

- `.claude/skills/marketing-os/SKILL.md` exists
- Broad task routing in `CLAUDE.md` points to `/marketing-os`
- Every skill named in the Sub-Agent Registry exists
- Skill frontmatter includes `name:` and `description:`
- Skills that write to CRM, monday, Slack, CMS, ad platforms, or email tools have approval rules
- Domain skills name their expected output or closeout format

### 6. Marketing Specificity

Flag generic or leftover template language that weakens the marketing positioning:

- Non-marketing examples in live docs
- Sales or analytics examples that are not framed as marketing dependencies
- "Team context" wording in user-facing starter copy where "Marketing Brain" would be clearer
- Generic issue-tracker or software-planning language unless the team actually uses it
- Example files living in `systems/owned/` or `systems/reference/`

## Output Format

Group findings by severity:

```markdown
## Marketing Brain Health Report

### Needs Immediate Attention
- Critical issues that can misroute work or create wrong outputs

### Should Fix Soon
- Stale docs, missing IDs, minor template drift

### Looking Good
- Healthy docs, complete references, clean skills

### Summary
X system docs checked, Y healthy, Z need attention.
Last full health check: [today's date]
```

## After The Check

Suggest concrete next steps:

- For stale docs: "Want me to open each one and walk you through a quick review?"
- For missing references: "Want me to help fill the board/channel schema?"
- For skill issues: "Want me to update the skill routing or create a task?"

Do not auto-fix findings unless the user asks.
