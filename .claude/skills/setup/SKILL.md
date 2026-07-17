---
name: setup
description: Use this skill when setting up a Marketing Brain for the first time, when the user says "set up my marketing brain", "configure marketing brain", "fill in placeholders", "initialize marketing brain", "onboard my marketing team", "set up", or when files still contain unfilled {{PLACEHOLDER}} values. This is the interactive onboarding wizard that replaces template placeholders with real marketing team data.
---

# Marketing Brain Setup Wizard

This skill personalizes the starter for a real marketing team. It replaces `{{PLACEHOLDER}}` values, creates first system stubs, and leaves the team with a usable Marketing Brain.

## Step 0: Check State

Scan for unfilled placeholders:

```bash
grep -r '{{' --include='*.md' --include='*.json' . | grep -v node_modules | grep -v '.git/' | grep -v '_example' | head -30
```

If no placeholders are found, tell the user setup appears complete and suggest `/health-check`.

If placeholders remain, continue.

## Step 1: Welcome

Say something like:

> Let's set up your Marketing Brain. I'll ask about your team, channels, work tracker, core marketing systems, and partner handoffs, then fill the repo automatically. It usually takes 5-10 minutes.
>
> We will need a few stable IDs from Slack and your work tracker. The starter defaults to monday.com, but you can use Notion or ClickUp if you document equivalent IDs and adapt tracker-specific skills.

## Step 2: Team Identity

Ask these together:

1. **Team name** - e.g. "Growth Marketing", "Lifecycle Marketing", "Product Marketing"
2. **Team slug** - suggest one from the name, e.g. `growth-marketing`
3. **Marketing function** - demand gen, lifecycle, product marketing, content, brand, web, partner marketing, marketing ops, integrated marketing, or mixed
4. **Group name** - e.g. "Marketing", "GTM", "Revenue"
5. **Marketing stack** - main tools and what they are used for, e.g. "HubSpot (CRM), Webflow (CMS), GA4/Looker (reporting), monday/Notion/ClickUp (work tracking)"

Store the marketing function in `{{TEAM_TYPE}}`.

## Step 3: People And Channels

Ask these together:

**First team member / champion**

1. Name
2. Role
3. Focus area
4. Slack ID - right-click name in Slack, then "Copy member ID"
5. Email
6. GitHub login, only if website or analytics PRs matter

**Manager** (skip if same person)

7. Name
8. Slack ID
9. Email

**Primary Slack channel**

10. Channel name without `#`
11. Channel ID - open channel details and scroll to the bottom, or copy the channel link and use the final ID segment

Optional but useful:

- Announcement channel
- Campaign launch channel
- Website request channel
- Marketing analytics channel

## Step 4: Boards And Operating Surfaces

Ask these together:

1. **Primary marketing work tracker ID** - monday board ID, Notion database ID, or ClickUp list ID
2. **Tracker workspace** - monday subdomain, Notion workspace, or ClickUp space/folder
3. **How work is organized** - planning cycles, groups, campaign calendar, or status/date/owner only
4. **Campaign calendar board ID** if the team uses one
5. **Content calendar / website / paid experiment board IDs** if they exist

Explain that exact column/field keys can be filled later in `references/monday_boards.md` or the adapted Notion/ClickUp tracker reference.

## Step 5: Marketing Systems

Ask for the systems the team owns or operates. Minimum one.

For each system, capture:

- Name
- One-line description
- Criticality: Critical, High, Medium, Low
- Owner or primary approver
- Main platform/source
- Main Slack channel or partner path

Suggested starter systems:

- CRM and lifecycle
- Marketing website / CMS
- Paid acquisition
- Campaign calendar
- Content operations
- Marketing measurement / attribution
- Events / webinars
- SEO / AI search

Also ask for partner-owned dependencies:

- Product analytics
- Sales CRM
- Brand library
- Data warehouse / analytics platform
- Product roadmap
- Web team

## Step 6: Build Replacement Map

Use the interview answers to replace:

| Placeholder | Value |
|---|---|
| `{{TEAM_NAME}}` | Team name |
| `{{TEAM_SLUG}}` | Confirmed slug |
| `{{TEAM_TYPE}}` | Marketing function |
| `{{GROUP_NAME}}` | Group name |
| `{{TECH_STACK}}` | Marketing stack |
| `{{TEAM_SLACK_CHANNEL}}` | Primary channel name |
| `{{TEAM_SLACK_CHANNEL_ID}}` | Primary channel ID |
| `{{MONDAY_TASKS_BOARD_ID}}` | Primary marketing tracker ID |
| `{{MONDAY_SPRINTS_BOARD_ID}}` | Planning cycle board ID, or `not used` |
| `{{MONDAY_WORKSPACE}}` | monday workspace subdomain, Notion workspace, or ClickUp space |
| `{{TEAM_LEAD_NAME}}` | First team member name |
| `{{TEAM_LEAD_GITHUB}}` | GitHub login or `not used` |
| `{{TEAM_LEAD_SLACK_ID}}` | First team member Slack ID |
| `{{TEAM_LEAD_EMAIL}}` | First team member email |
| `{{MANAGER_NAME}}` | Manager name |
| `{{MANAGER_SLACK_ID}}` | Manager Slack ID |
| `{{MANAGER_EMAIL}}` | Manager email |
| `{{GITHUB_ORG}}` | GitHub org or `not used` |
| `{{GITHUB_TEAM_LOGINS}}` | Pipe-separated logins, or `not used` |
| `{{SETUP_DATE}}` | Today's date YYYY-MM-DD |

For any placeholder not relevant to the team, use `not used` rather than leaving it blank.

## Step 7: Apply Placeholder Replacements

For every file containing setup placeholders:

1. Read the file.
2. Replace all `{{PLACEHOLDER}}` values from the map.
3. Preserve markdown structure and comments.

Process at least:

- `CLAUDE.md`
- `README.md`
- `references/team.md`
- `references/slack.md`
- `references/monday_boards.md`
- `references/other_teams.md`
- `.claude/skills/daily-brief/SKILL.md`
- `.claude/skills/marketing-brief/SKILL.md`

## Step 8: Populate Core Tables

### Systems Reference in `CLAUDE.md`

For each owned system:

```markdown
| System Name | `systems/owned/system-slug.md` |
```

For each partner-owned dependency:

```markdown
| System Name (owned by Team) | `systems/reference/system-slug.md` |
```

### Team roster in `references/team.md`

Add the first team member and any additional teammates with focus areas.

### Slack reference

Add channels mentioned during setup with purpose and notes.

### Work tracker reference

Add any campaign, content, website, paid, or analytics monday boards, Notion databases, or ClickUp lists the user named.

## Step 9: Create System Doc Stubs

Create `systems/owned/<slug>.md` for each owned system using the full marketing system template:

```markdown
<!-- last-reviewed: YYYY-MM-DD -->
# System Name

> One-line description from setup.

## Overview
[To be filled in - say "teach me about System Name" or run /knowledge-interview]

## How Claude Works With This
| Action | How |
|--------|-----|
| Make changes | Platform/admin path or monday board |
| Investigate | Dashboard, report, owner, or Slack channel |
| Publish / launch | Approval path or scheduler |

## Platforms / Data Sources
| Source | What it contains | Owner |
|--------|------------------|-------|
| [Platform] | [To be filled in] | [Owner] |

## Operating Model
- Owner: [from setup]
- Approval path: [To be filled in]
- Intake path: [To be filled in]

## Key Surfaces
- [To be filled in]

## Audience / Segmentation
- [To be filled in]

## Measurement
| Metric | Source | Notes |
|--------|--------|-------|
| [To be filled in] | | |

## Known Issues / Failure Modes
| Issue | Symptoms | Resolution |
|-------|----------|------------|
| [To be filled in] | | |

## Related Systems
- **Upstream:** [To be filled in]
- **Downstream:** [To be filled in]
- **Partner teams:** [To be filled in]

## Pointers
- **Skills:** [To be filled in]
- **Dashboards:** [To be filled in]
- **Boards:** [To be filled in]
- **Channels:** [from setup if known]
```

For partner-owned dependencies, create `systems/reference/<slug>.md` with the light template.

Set `last-reviewed` to today's date.

## Step 10: Replace The README

After setup, replace `README.md` with the post-setup version from `.claude/skills/setup/README-INSTANCE.md`:

1. Read `README-INSTANCE.md`.
2. Replace placeholders using the same map.
3. Populate the systems table with created docs.
4. Keep the skills table focused on the active marketing workflows.

## Step 11: Summary And Commit

Before committing, show:

```markdown
Setup complete. Here's what changed:

- Filled X placeholders across Y files
- Created Z marketing system docs
- Added N channels / boards / partner paths
- Updated README for this team

Ready to commit these changes?
```

Ask for confirmation. If approved:

```bash
git add -A
git commit -m "init: set up marketing brain for [team name]"
```

## Step 12: What's Next

After commit, suggest:

```markdown
Your Marketing Brain is ready.

- Try "good morning" for the first daily brief.
- Say "teach me about [most important system]" to fill the first system doc.
- Fill exact tracker field keys in references/monday_boards.md, whether the team uses monday, Notion, or ClickUp.
- Add partner teams in references/other_teams.md.
- Run /knowledge-interview when you have 15 minutes.
- Run /retro after the next campaign or workflow that teaches something useful.
```

## Step 13: Optional Cleanup

Ask whether to remove `/setup` after the team is fully configured. Only remove it if the user confirms.
