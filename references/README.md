# References

Stable lookup data used by marketing skills and agents. These files hold IDs, owner paths, channel names, board schemas, and partner contacts that rarely change but are needed constantly.

## What Belongs Here

- Work tracker IDs and fields: monday board IDs/column keys by default, or Notion database IDs / ClickUp list IDs and exact status labels
- Slack channel IDs, user groups, announcement channels, and intake channels
- Marketing team roster and focus areas
- Partner team contacts, intake paths, and escalation channels
- Links to source-of-truth folders or views that multiple skills reuse

## What Does Not Belong Here

- Live campaign metrics or current performance numbers
- Feedback or action items that should become tasks or skill updates
- Process documentation that belongs in a skill
- Platform behavior that belongs in a system doc
- Duplicate rosters or copied partner docs

## Single Source Of Truth

**Team roster:** `team.md` is authoritative. Other files should point to it instead of duplicating people lists.

**Live data:** keep it in the tool that owns it. References should tell Claude where to look and how to interpret the stable schema.
