# Slack Reference

> Channel IDs and user groups used by skills and agents. For the people roster, see `references/team.md` (single source of truth - don't duplicate it here).

## Team Channels

| Channel | ID | Purpose | Notes |
|---------|----|---------|-------|
| `#{{TEAM_SLACK_CHANNEL}}` | `{{TEAM_SLACK_CHANNEL_ID}}` | Primary team channel | |
<!-- Add more channels as skills need them. Examples: -->
<!-- | `#marketing-announcements` | `C0XXXXXXX` | Outbound announcements | Public | -->
<!-- | `#website-requests` | `C0XXXXXXX` | Website intake | Cross-team | -->

## Cross-Team Channels

<!-- Channels owned by other teams that your workflows read or post to. -->

| Channel | ID | Owner team | When to use |
|---------|----|-----------|-------------|

## User Groups

<!-- Slack user group handles (@handles) used in messages. -->

| Handle | Who it pings |
|--------|--------------|

## Notes

- To find a channel ID: right-click the channel name > "View channel details" > scroll to the bottom. Channel IDs start with `C`.
- **Private channels:** a skill reading a private channel only works if the runner's Slack connection is a member. `channel_not_found` usually means "not a member", not "channel deleted" - document membership constraints here so agents handle it gracefully.
