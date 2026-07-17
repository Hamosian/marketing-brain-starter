# Work Tracker Reference

> Work tracker IDs, workspace info, group/view/list rules, and field keys used by marketing skills. The starter is wired for monday.com by default. If your team uses Notion or ClickUp, document the equivalent database/list IDs and fields here, then adapt tracker-specific skills/tools.

**Workspace:** `{{MONDAY_WORKSPACE}}.monday.com` by default, or the equivalent Notion workspace / ClickUp space-folder path
**Last verified:** {{SETUP_DATE}}

## Boards / Databases / Lists

| Board | ID | Purpose |
|-------|----|---------|
| Marketing Tasks | `{{MONDAY_TASKS_BOARD_ID}}` | Primary work intake and execution board |
<!-- Add more boards as needed. Examples: -->
<!-- | Campaign Calendar | `123456789` | Launch dates, campaign milestones, owners | -->
<!-- | Content Calendar | `123456789` | Editorial planning and publishing | -->
<!-- | Website Requests | `123456789` | Landing pages, CRO, CMS updates | -->
<!-- | Paid Experiments | `123456789` | Budgeted tests and channel experiments | -->

## How Work Is Organized

<!-- Pick one and document it. Skills like /good-morning and /pm-story read this:
- CYCLES: marketing runs active work in planning cycles; filter by the current cycle.
- GROUPS: the board uses groups such as "This Week", "In Flight", "Blocked", "Backlog", or "Launched";
  list which group IDs count as active and which should be ignored.
- CAMPAIGN CALENDAR: launch timing lives on a separate campaign board; link tasks to campaign rows.
- NONE: filter by status, due date, owner, and priority only.
-->

## Column Keys - Marketing Tasks Board

Column or field keys are tracker-specific. Fill these in by inspecting the board, Notion database, or ClickUp list, because skills only set fields documented here.

| Column | Key | Type | Labels / notes |
|--------|-----|------|----------------|
| Status | `status` | status | e.g. `New`, `In Progress`, `Blocked`, `Ready for Review`, `Done` - use exact labels |
| Owner | `person` | people | numeric monday user IDs via `list_users_and_teams`, or equivalent Notion/ClickUp user IDs |
<!-- | Priority | `priority` | status | e.g. `Critical`, `High`, `Medium`, `Low` | -->
<!-- | Work type | `type` | status | e.g. `Campaign`, `Content`, `CRM`, `Website`, `Paid`, `Analytics`, `Request` | -->
<!-- | Channel | `channel` | dropdown/status | e.g. `Email`, `Paid Social`, `SEO`, `Web`, `Events`, `Partner` | -->
<!-- | Campaign | `campaign` | connect_boards/text | Link to campaign calendar row or campaign name | -->
<!-- | Launch date | `date` | date | Date the work goes live or is due | -->
<!-- | Approver | `approver` | people | Required for public-facing or customer-facing work | -->

## Gotchas

- monday board IDs are the number in the URL after `/boards/`; Notion and ClickUp IDs should be copied from their database/list URLs or API metadata.
- Status columns require the exact label text that exists on the board.
- Person columns in `create_item` need `{"personsAndTeams": [{"id": <numeric-id>, "kind": "person"}]}`.
- Document parked groups clearly. Otherwise daily briefs may treat backlog or old launch tasks as active work.
- If a campaign lives on another board, document the relationship here before asking skills to create linked work.
