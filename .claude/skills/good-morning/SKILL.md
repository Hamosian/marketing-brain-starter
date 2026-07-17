---
name: good-morning
description: Use this skill when the user says "good morning", "morning brief", "daily brief", "daily standup", "catch me up", "what happened overnight", "what's going on today", "start of day", or wants a daily summary of active monday work, team updates, Slack activity, open risks, and recommended actions.
---

# Good Morning Brief

Generate a daily morning brief for the team member. The goal is to give them everything they need to orient themselves in 60 seconds: their active work, urgent unowned items, what needs a decision, and what's happening in Slack.

Fetch ALL data in parallel before rendering anything. Speed matters here - this is the first thing someone does in the morning.

---

## Step 1: Read Source Registry and Fetch Everything in Parallel

Read the **Morning Brief Sources** table from `CLAUDE.md`. For each source where Enabled = "Yes" (not commented out), launch the corresponding fetch in parallel. Skip sources that are commented out or not present.

### Source: Active tasks (monday)

Use `mcp__monday-api__get_board_items_page` on the configured tasks board.

Configure the filters and columns based on your team's board schema in `references/monday_boards.md`. At minimum:
- Filter to tasks owned by the current user
- Filter to statuses that are not Done, Closed, or Cancelled
- **If the team runs sprints**, filter to the active sprint (`get_sprints_metadata`). **If not**, use status + due date + owner instead - and if the board uses manual groups (e.g. `Backlog`, `On Hold`) to park long-idle items, exclude those groups, or overdue/workload counts will be inflated with stale, already-shelved work. Document which approach your board uses in `references/monday_boards.md`.
- Prioritize items due today, due this week, overdue, or marked P0/P1 - computed over the filtered active set
- Fetch the columns you want shown in the brief: owner, status, priority, type, due date, name, board URL

### Source: Unowned bugs (monday)
Same board, different filter: bug or issue items with no owner and status not Done/Closed. Look up type label names or IDs from `references/monday_boards.md` when available.

### Source: Slack (slack)
```
slack_read_channel(channel_id: "<channel_id_from_config>", limit: 50, response_format: "concise")
```

If additional channels are added to `CLAUDE.md`, read them in parallel with the team channel.

**Private channels depend on who runs the brief.** If reading the configured channel returns `channel_not_found`, the runner's Slack connection isn't a member - the channel is not necessarily archived or renamed. Skip the source, substitute a channel the runner can access from `references/slack.md`, and say so in the brief instead of failing.

### Source: Open PRs (github)
Only if enabled in the source registry. For each repo listed in the config:
```bash
gh pr list --repo <org>/<repo> --state open \
  --json number,title,author,createdAt,reviewRequests,isDraft \
  | jq '[.[] | select(.isDraft == false) | select(.author.is_bot == false)] | .[:5]'
```

**Team GitHub logins** (for filtering shared repos): Read the `GitHub logins` field from the Team section in CLAUDE.md (pipe-separated list, e.g. `user1|user2|user3`).

**Bot/noise exclusions**: `dependabot` and any `is_bot == true` accounts. Add team-specific CI bot logins here as needed.

### Source: Merged PRs (github)
Only if enabled in the source registry. Compute the cutoff as 6 AM UTC yesterday:
```bash
CUTOFF=$(date -u -v-1d '+%Y-%m-%dT06:00:00Z' 2>/dev/null || date -u -d 'yesterday 06:00' '+%Y-%m-%dT06:00:00Z')
gh pr list --repo <org>/<repo> --state merged --limit 50 \
  --json number,title,author,mergedAt \
  | jq --arg cutoff "$CUTOFF" '[.[] | select(.author.is_bot == false) | select(.mergedAt > $cutoff)]'
```

---

## Step 2: Render the Brief

**Important:** Only render sections for sources that were enabled and fetched. If a source is not in the Morning Brief Sources table (or is commented out), skip that entire section silently. Do not show empty sections or "not configured" messages.

Use this exact structure. Keep it tight - this is a morning brief, not a report.

### Header
```
# Good Morning Brief - [Weekday, Month DD, YYYY]
```

---

### Active Work - Your Tasks

Start with a one-line workload summary:

```
Active work: [N] open, [X] overdue, [Y] due this week, [Z] P0/P1
```

Then a table of tasks:

| Task | Status | Priority | Due |
|------|--------|----------|-----|
| [name](url) | emoji + label | label | date |

Status emojis: In Progress, Pending Review, Ready to start, Done, Stuck

One short insight below the table (1-2 sentences max). Flag overdue P0/P1 work, too many simultaneous "In Progress" items, or stale "New" investigations. Keep it actionable, not preachy.

---

### Unowned Bugs

If none: "> No unowned bugs or issues need assignment."

If any, a table:
| Bug | Age |
|-----|-----|
| [name](url) | X days |

Note: if the bug has been sitting for >7 days, flag it - it needs an owner or a close decision.

---

### Slack Highlights

**#team-channel** (last 48h)

Pull only the last 48 hours of messages. List 3-5 key items max. Each item is one line:
- Lead with an emoji that fits the vibe
- Name the person
- One-sentence summary
- If it's an open question or needs a response, add **unanswered** or **needs decision** in bold at the end

---

### PRs Open for Review

Single combined table across all repos, sorted by age ascending (newest first):

| # | Repo | Title | Author | Age |
|---|------|-------|--------|-----|
| [#N](url) | repo-name | title | Name | 3d |

- Mark your own PRs with **you** - those need someone else's review.
- Flag PRs older than 7 days.
- Skip bots and non-team contributors (use the GitHub login allowlist above).

If no team PRs open: "> No open team PRs right now."

---

### Merged Yesterday

Narrative format, grouped by system area. Last 24 hours, team only.

For each area with merged PRs, write a header with an emoji, then one bullet per person who merged something. Link PR numbers inline (e.g. [#123](url)). Highlight if it was you with **you**.

<!-- Customize these system groupings for your team. Examples: -->
<!-- **Website** - landing pages, CRO tests -->
<!-- **Automation** - CRM workflows, syncs -->
<!-- **Team** - team context, skills, docs -->

One line at the bottom: "N merges across the team yesterday."

If none: "> No team merges in the last 24 hours."

---

### Suggested Actions

After rendering the full brief, present 3-5 concrete action items derived from the data. Use `AskUserQuestion` with `type: "select"` to let them pick what to act on first.

Options should be specific and actionable, pulled directly from the brief. Include a "Nothing, I'm good" option as the last choice. If the user picks something, help them act on it immediately.

---

## Key Principles

- **Speed over completeness.** Fetch everything in parallel. Don't paginate Slack unless the first page gives almost nothing.
- **Filter out parked work.** Whether via sprints or manual groups, separate active work from backlog before computing overdue/workload numbers - see `references/monday_boards.md`.
- **Team-only GitHub data.** If PRs are enabled, use the GitHub login allowlist strictly. A non-team PR in the table is confusing and wrong.
- **48h for Slack, since yesterday morning (6 AM UTC) for merged PRs, most recent 5 for open PRs.** Only applies to enabled sources.
- **One line per Slack item.** If you can't summarize it in one line, it's not important enough for the morning brief.
- **No padding.** If a section is empty, say so cleanly and move on. Don't write "I was unable to find any..." - just say "No unowned bugs today."
- **Emoji in section headers** makes the brief scannable at a glance. Use them.
