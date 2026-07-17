# Monday Boards Reference

> Board IDs, workspace info, and column keys used by skills. Verify this data periodically - `/health-check` flags it when stale.

**Workspace:** `{{MONDAY_WORKSPACE}}.monday.com`
**Last verified:** {{SETUP_DATE}}

## Boards

| Board | ID | Purpose |
|-------|----|---------|
| Team Tasks | `{{MONDAY_TASKS_BOARD_ID}}` | Primary task board |
<!-- Add more boards as needed. Examples: -->
<!-- | Sprints | `<sprints-board-id>` | Sprint board (skip if the team doesn't run sprints) | -->
<!-- | Planning | `123456789` | Quarterly/annual planning | -->

## How Work Is Organized

<!-- Pick one and document it - skills like /good-morning and /pm-story read this:
- SPRINTS: the team uses monday sprints; filter active work via get_sprints_metadata.
- GROUPS: the team uses manual groups (e.g. weekly buckets, "Backlog", "On Hold");
  list the group IDs to include/exclude when computing active work.
- NONE: filter by status + due date + owner only.
-->

## Column Keys - Team Tasks Board

Column keys are board-specific. Fill these in by inspecting the board (`get_board_info`), because skills only set columns documented here.

| Column | Key | Type | Labels / notes |
|--------|-----|------|----------------|
| Status | `status` | status | e.g. `New`, `In Progress`, `Done` - use exact labels |
| Owner | `person` | people | numeric user IDs via `list_users_and_teams` |
<!-- | Priority | `priority` | status | e.g. `P0`-`P3` | -->
<!-- | Type | `type` | status | e.g. `Bug`, `Task`, `Request` | -->
<!-- | Due date | `date` | date | | -->

## Gotchas

- Board IDs are the number in the URL after `/boards/`.
- Status-type columns require the **exact** label text that exists on the board.
- Person columns in `create_item` need `{"personsAndTeams": [{"id": <numeric-id>, "kind": "person"}]}` - the `person-<id>` string form only works in filters.
