---
name: health-check
description: Use this skill when the user wants to check the health of the team context, find stale docs, missing fields, or template compliance issues. Triggered by "health check", "check repo health", "stale docs", "team context health", "are our docs up to date", "what needs updating", "doc hygiene", "review system docs". Good to run during sprint retros or after major infrastructure changes.
---

# Team Context Health Check

Scans the team context for staleness, template drift, and missing content. Reports what needs attention so the team can keep the knowledge base accurate.

## What to Check

### 1. System Doc Staleness

Read all files in `systems/owned/` and `systems/reference/`. For each file:

1. Look for `<!-- last-reviewed: YYYY-MM-DD -->` on the first line
2. If missing: flag as **missing review date**
3. If present: calculate days since last review. Flag as **stale** if older than 90 days

Present results as a table:

```
System Doc Health:

| System | Last Reviewed | Status |
|--------|--------------|--------|
| ai-brain.md | 2026-03-31 | OK (0 days ago) |
| airflow.md | 2025-12-15 | STALE (107 days ago) |
| tableau.md | (missing) | NO DATE |
```

### 2. TODO / Placeholder Scan

Search production knowledge files in `systems/owned/`, `systems/reference/`, and `references/` for:
- `<!-- TODO` comments
- Empty sections (header followed immediately by another header or end of file)
- Placeholder text like `TBD`, `TODO`, `FIXME`

Flag each finding with file path and line number.

Skip `systems/README.md` and `systems/examples/`; those are templates and examples, not live operating context.

### 3. Template Compliance

For each system doc, check which template it should follow:
- If the doc's Pointers section says "Investment: Maintain Only" -> light template
- Otherwise -> full template

Check required sections are present:

**Full template required sections:** Overview, Repos, Architecture, Key Entry Points, Related Systems, Pointers
**Light template required sections:** Overview, What the Team Owns, What the Team Does NOT Own, When It Breaks, Related Systems, Pointers

Flag missing sections.

### 4. Reference Data Freshness

Check `references/monday_boards.md` for the "last verified" date. Flag if older than 90 days.

### 5. Roster Integrity

Check `references/team.md` for completeness:
- Every team member has a non-empty Slack ID
- Every team member has an email or an explicit "unknown" note
- Every team member has a GitHub login only if a GitHub login column exists or GitHub sources are enabled
- `references/slack.md` still points to `team.md` for the roster (link integrity)

### 6. Marketing OS / Sub-Agent Integrity

Check the Marketing OS layer:
- `.claude/skills/marketing-os/SKILL.md` exists
- Broad task routing in `CLAUDE.md` points to `/marketing-os`
- Every sub-agent named in the Marketing OS registry has a corresponding `.claude/skills/<name>/SKILL.md`
- Sub-agent skills include an "Output Contract" section
- Connector sub-agents have clear approval rules for writes

### 7. Template Residue

Flag example or template files that can pollute routing:
- Any `_example-*.md` file under `systems/owned/` or `systems/reference/`
- Placeholder snippets in always-loaded files: `README.md`, `CLAUDE.md`, `references/*.md`
- Generic setup instructions that conflict with the team's actual operating model, such as sprint-only guidance for a team that doesn't run sprints

## Output Format

Group findings by severity:

```
## Team Context Health Report

### Needs Immediate Attention
- [list of critical issues: missing dates, TODOs in critical systems, template violations]

### Should Fix Soon
- [list of stale docs, minor template drift]

### Looking Good
- [count of healthy docs, compliant templates]

### Summary
X system docs checked, Y healthy, Z need attention.
Last full health check: [today's date]
```

## After the Check

Suggest specific next steps:
- For stale docs: "Want me to open each one so you can review and update the `last-reviewed` date?"
- For TODOs: "Want me to try filling these in, or should we create tasks for them?"
- For template violations: "Want me to restructure these docs to match the template?"

Don't auto-fix anything - present findings and let the user decide what to address.
