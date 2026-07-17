---
name: marketing-brief
description: "ALWAYS use this skill - do not call Monday MCP tools directly - when the user wants to create, document, update, or sharpen a marketing task, campaign brief, content request, CRM change, website request, paid experiment, analytics request, or board item. Triggered by \"marketing-brief\", \"create a task\", \"add this to the board\", \"write this up\", \"turn this into a brief\", \"log this request\", \"track this\", \"open a task\", \"document this task\", \"update this task\", \"launch task\", \"campaign task\", or any message that includes a Monday task URL with intent to improve the task context."
user-invocable: true
---

# Marketing Work Brief

Use this skill to turn a loose marketing request into a useful monday item. The output should read like something a campaign owner, channel owner, designer, analyst, or lifecycle marketer can act on without another meeting.

The default implementation uses monday.com MCP calls. If the team uses Notion or ClickUp instead, keep the same brief structure but adapt the load/write steps to the team's configured tracker connector and field reference.

Two cases:

- **New item:** The user has an idea or request with no monday item yet.
- **Existing item:** The user points to a URL, item ID, or task name that already exists but needs a better brief.

The final monday content should include the practical marketing context: Why, Audience, Message/Offer, Channel/Surface, Done When, and Open Questions. Omit sections that truly do not apply, but never leave the item as a bare title.

## Step 1: Load Existing Task Context

If the user gives a monday URL, item ID, or task name, load the full monday context:

- Item detail from the tasks board in `references/monday_boards.md`, with description and columns included
- Item comments or updates
- Linked campaign, epic, or parent item if the board schema documents one
- Nearby related items on the same campaign, channel, or group when useful

If this is a new item, capture the user's wording and continue.

## Step 2: Identify The Marketing System

Read `CLAUDE.md` and match the request against the Systems Reference table.

Common matches:

- CRM, lifecycle, email, nurture, scoring, routing -> `systems/owned/crm-lifecycle.md`
- Website, landing page, CMS, CRO, forms -> `systems/owned/marketing-website.md`
- Paid, budget, experiment, creative, channel -> `systems/owned/paid-acquisition.md`
- Campaign, launch, brief, calendar -> `systems/owned/campaign-calendar.md`
- Reporting, attribution, dashboard, readout -> `systems/owned/marketing-measurement.md`

Read every relevant system doc. If no system doc exists, say that the system is not documented yet and use `README.md`, `references/`, and the user's context as the fallback.

## Step 3: Gather Supporting Context

Use the system doc to find boards, dashboards, channels, owners, and source systems. Gather only context that helps write the brief.

Prioritize:

- Existing monday items for the same campaign, channel, launch, or platform
- Relevant Slack discussion in the team channel or documented partner channel
- System doc sections for known risks, approval rules, audience rules, and measurement caveats
- Live source links the user provided, such as brief docs, dashboard URLs, CMS pages, CRM lists, or asset folders

Do not copy live metrics or audience counts into the repo. For the monday item, summarize what matters and link to the source when available.

## Step 4: Walk Through The Brief

Walk through the key sections with the user one at a time. Keep each message short and practical.

Use this order:

1. **Why** - the business reason, user/customer problem, campaign goal, or internal need
2. **Audience** - who this is for and any segment/suppression caveats
3. **Message / Offer** - the core promise, CTA, asset, or change being requested
4. **Channel / Surface** - where it ships: email, web, paid, SEO, social, sales enablement, analytics, etc.
5. **Done When** - observable completion criteria

Example:

```markdown
**Why - here's my read:**
This is about improving webinar follow-up so high-intent attendees get routed before interest cools.

Sound right, or is there a different pain point driving it?
```

Wait for confirmation or correction before moving to the next section. Once the sections are confirmed, continue without asking for one more final confirmation.

## Step 5: New Item Metadata

Skip this step for existing items unless the user asked to update metadata.

For a new item, infer defaults from `references/monday_boards.md` and ask one compact question only for missing essentials:

- Board: default to Marketing Tasks unless another board is clearly documented
- Planning bucket: current week/cycle, this month/quarter, backlog, or urgent
- Owner: current user by default, unassigned, or another named person
- Priority: Medium by default, then High/Critical/Low if the request implies it
- Work type: Campaign, Content, CRM, Website, Paid, Analytics, Event, Request, or Other
- Channel: optional, based on the board's documented column
- Campaign: optional, if a campaign board/link is documented
- Launch or due date: optional, if the user gave one or the work has an obvious date

Only set monday columns whose keys and labels are documented in `references/monday_boards.md`. If a column is not documented, omit it and mention the missing schema after creation.

## Step 6: Draft The Final Brief

Assemble the confirmed sections.

```markdown
## Why
{1-2 sentences}

## Audience
{segment, persona, account group, region, lifecycle stage, or "internal team"}

## Message / Offer
{core message, CTA, asset, experiment, change, or deliverable}

## Channel / Surface
{where this ships or what system changes}

## Done When
- [ ] {observable scenario}
- [ ] {observable scenario}
- [ ] {observable scenario}

## Open Questions
- {question}

---
*Documented via Claude Code on {today's date}*
```

Keep the copy tight. The brief should help execution, not become a campaign strategy doc.

## Step 7: Write To Monday

**Task name for new items:** Generate a short, human-sounding name, 5-8 words max. Use lowercase except proper nouns.

Good examples:

- `qa webinar follow-up routing`
- `refresh enterprise landing page proof`
- `audit nurture suppression rules`
- `launch Q3 paid test readout`

**New item:** call `create_item` using the selected board ID and only documented column values.

**Existing item:** use the existing item ID.

Set the item description with `all_monday_api` using GraphQL variables, not inline markdown:

```graphql
mutation SetDesc($itemId: ID!, $markdown: String!) {
  set_item_description_content(item_id: $itemId, markdown: $markdown) {
    success
    error
    block_ids
  }
}
```

Check `success` before telling the user the description was set.

If monday returns an internal error or the board type does not support item descriptions, post the same brief as the first update via `create_update`. Convert markdown to simple HTML before posting. Tell the user it landed in updates only after the update returns an ID.

## Step 8: Confirm

Return the item URL:

```text
https://{{MONDAY_WORKSPACE}}.monday.com/boards/{board_id}/pulses/{item_id}
```

Also mention any metadata you could not set because the board schema was not documented.
