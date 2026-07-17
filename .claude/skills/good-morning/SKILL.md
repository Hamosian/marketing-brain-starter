---
name: good-morning
description: Use this skill when the user says "good morning", "morning brief", "daily brief", "daily standup", "catch me up", "what happened overnight", "what's going on today", "start of day", or wants a daily marketing summary of active tracker work, open blockers, Slack activity, upcoming launches, risks, and recommended next actions.
---

# Good Morning Marketing Brief

Generate a daily brief that helps a marketer orient in 60 seconds: active work, urgent blockers, launch timing, Slack decisions, and the next few moves.

Fetch all enabled sources in parallel before rendering. Speed matters because this is the first check-in of the day.

## Step 1: Read Source Registry

Read the **Morning Brief Sources** table from `CLAUDE.md`. For each source where Enabled = "Yes", fetch the corresponding data. Skip commented-out or missing sources silently.

## Source Handling

### Active Marketing Work (tracker)

Use the configured board, database, or list from `references/monday_boards.md`.

Filter based on the documented board schema:

- Owned by the current user when possible
- Status is not Done, Closed, Cancelled, Launched, or Parked
- If the board uses planning cycles, filter to the active cycle
- If the board uses groups, exclude parked groups such as Backlog, Ideas, On Hold, or Launched
- Prioritize overdue, due today, due this week, blocked, or Critical/High priority work

Fetch fields that help the brief: owner, status, priority, work type, channel, campaign, due or launch date, name, and URL.

### Unowned Requests Or Blockers (tracker)

Use the same board unless another source is configured. Look for:

- Items with no owner
- Items in Blocked or Needs Decision
- Intake/request items older than the team's expected triage window
- Launch-adjacent work missing an approver or date

### Slack

Read the configured team channel and any enabled partner channels.

If a private channel returns `channel_not_found`, the runner's Slack connection may not be a member. Skip that source and say which channel could not be read.

Summarize only the last 48 hours unless the source config says otherwise.

### Open PRs / Merged PRs

Only include if enabled in `CLAUDE.md`. This is mainly useful for website, analytics, or technical marketing work.

Use the GitHub login allowlist in `references/team.md` when filtering shared repos. Skip bots and unrelated contributors.

## Step 2: Render The Brief

Only render sections for sources that were enabled and fetched. Do not show empty "not configured" sections.

Use this structure:

```markdown
# Good Morning Brief - [Weekday, Month DD, YYYY]

## Active Work
Active work: [N] open, [X] blocked, [Y] due this week, [Z] high priority

| Work | Status | Priority | Due / Launch |
|------|--------|----------|--------------|
| [name](url) | label | label | date |

Insight: [one short sentence about the most important pattern]

## Open Blockers
| Item | Owner | Age | Why it matters |
|------|-------|-----|----------------|

## Slack Highlights
- Person: one-sentence summary. Mark **needs decision** or **needs response** when relevant.

## Upcoming Launches
| Launch | Owner | Date | Risk |
|--------|-------|------|------|

## Suggested Moves
1. [specific action]
2. [specific action]
3. [specific action]
```

If a section has no items, say so in one line and move on.

## Suggested Actions

End with 3-5 concrete actions derived from the data. If the user picks one, help immediately:

- Create or update a tracker task with `/pm-story`
- Draft a Slack reply
- Open the relevant system doc
- Prepare a quick triage table
- Suggest `/retro` if a new learning surfaced

## Key Principles

- **Brief, not report.** Lead with what needs attention.
- **Active work only.** Do not inflate workload with parked backlog.
- **Marketing framing.** Name campaign, channel, launch, audience, or metric when available.
- **No unsupported performance claims.** If metrics are included, name the source and freshness.
- **No padding.** If nothing needs attention, say that cleanly.
