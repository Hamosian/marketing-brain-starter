# Slack Reference

> Channel IDs, user groups, and message rules used by marketing skills. For people, use `references/team.md`.

## Team Channels

| Channel | ID | Purpose | Notes |
|---------|----|---------|-------|
| `#{{TEAM_SLACK_CHANNEL}}` | `{{TEAM_SLACK_CHANNEL_ID}}` | Primary marketing team channel | Daily work, decisions, blockers |
<!-- Add more channels as skills need them. Examples: -->
<!-- | `#marketing-announcements` | `C0XXXXXXX` | Company-facing marketing announcements | Public, approved posts only | -->
<!-- | `#campaign-launches` | `C0XXXXXXX` | Launch coordination and day-of updates | Include launch owner in posts | -->
<!-- | `#website-requests` | `C0XXXXXXX` | Website intake and handoffs | Cross-team with web/dev | -->
<!-- | `#marketing-analytics` | `C0XXXXXXX` | Reporting questions and metric caveats | Partner-owned by Data | -->

## Cross-Team Channels

<!-- Channels owned by partner teams that marketing workflows read or post to. -->

| Channel | ID | Owner team | When to use |
|---------|----|------------|-------------|

## User Groups

<!-- Slack user group handles used in messages. -->

| Handle | Who it pings | When to use |
|--------|--------------|-------------|

## Message Rules

- Draft external-facing or company-wide posts before sending.
- Reply in-thread when acting on an existing discussion.
- End agent-sent Slack messages with `_Posted by the team's AI agent_`.

## Notes

- To find a channel ID: right-click the channel name, choose "View channel details", and scroll to the bottom. Channel IDs start with `C`.
- Private channels only work when the runner's Slack connection is a member. `channel_not_found` usually means "not a member", not "channel deleted".
