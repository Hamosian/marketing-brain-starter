# Team Roster

> Single source of truth for team membership. Other files should link here, not duplicate this table.

**Team:** {{TEAM_NAME}}
**Group:** {{GROUP_NAME}}
**Last updated:** {{SETUP_DATE}}

## Team

| Name | Role | Slack ID | Email |
|------|------|----------|-------|
| {{TEAM_LEAD_NAME}} | Lead | `{{TEAM_LEAD_SLACK_ID}}` | {{TEAM_LEAD_EMAIL}} |
<!-- Add team members below. One row per person. -->

## Manager

| Name | Slack ID | Email |
|------|----------|-------|
| {{MANAGER_NAME}} | `{{MANAGER_SLACK_ID}}` | {{MANAGER_EMAIL}} |

## GitHub Logins

Used by skills that filter PRs to team members only (pipe-separated): `{{GITHUB_TEAM_LOGINS}}`

## Notes

- To find someone's Slack ID: right-click their name in Slack > "Copy member ID".
- Keep this table current - `/health-check` flags members with missing Slack IDs or emails.
