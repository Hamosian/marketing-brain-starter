---
name: pm-story
description: "ALWAYS use this skill - do not call Monday MCP tools directly - when the user wants to write, document, update, or create a product story or task. Triggered by ANY of these: \"pm-story\", \"write a story\", \"document this task\", \"update this task\", \"fill in this task\", \"write up this task\", \"log this idea\", \"track this\", \"add this to the board\", \"open a task for X\", \"create a task\", \"add a task\", \"log an issue\", \"I found a bug\", \"track this issue\", \"add this to the sprint\", or any message that includes a Monday task URL with intent to document or fill in product context."
user-invocable: true
---

# PM Story

Two cases - detect from the user's message:

* **New task:** User has an idea with no Monday item yet. Create one.
* **Existing task:** User points to a URL or name. The item exists but may only have a title.

In both cases, the output is always the same: a Monday item description with Why / What / Done When / Open Questions - grounded in actual system context, not guesswork.

The goal is to exhaust every available context source before asking the user anything.

---

## Step 1: Load the Task (existing tasks only)

If the user gives a URL or name, load the full Monday context in parallel:

* **Item detail** - `get_board_items_page` on the tasks board (ID in `references/monday_boards.md`) with the item ID, `includeItemDescription: true`, `includeColumns: true`
* **Item comments** - `get_updates` on the item ID
* **Linked epic** - if the board has an epic/connect column with a linked item, fetch it with `includeItemDescription: true`. Also fetch other tasks in the same epic (gives scope and what's being built around this).

If it's a new task, note what the user described and move to Step 2.

---

## Step 2: Identify the System

Keyword-match the task name and any description against the systems table in CLAUDE.md. Read the matching system file - this is mandatory. It contains platform names, config locations, and architecture context needed to ground the brief.

<!-- Customize this table with your team's systems. Examples: -->
<!-- Marketing: -->
<!-- | CRM, lifecycle, workflows | `systems/owned/crm.md` | -->
<!-- | Website, landing pages, CRO | `systems/owned/marketing-website.md` | -->
<!-- | Paid, campaigns, ad platforms | `systems/owned/paid-acquisition.md` | -->

If the task spans multiple systems, read all relevant files. If nothing matches, read `README.md` and use the systems table there.

---

## Step 3: Saturate Context (all in parallel)

Use the system doc to find repos, platforms, and Slack channels. Then run all of these at once:

### 3a. Deep context (domain-specific)

**If the matching system doc has a `Repos` section** (engineering/data teams):
Use `Glob` and `Grep` on the local repo path (from the system doc) to find files related to the task. Read 2-4 relevant files. You are looking for **product understanding**, not implementation details:
* What does the feature currently do? What can users configure, see, or trigger?
* What are the current entry points / user-facing surfaces?
* Are there any comments, open flags, or notes that hint at known gaps or planned changes?

Do NOT surface file names, function names, or code-level details in the brief. Translate what you find into product/user language.

**If the system doc has NO `Repos` section** (most marketing teams):
Skip code search. Instead, increase the weight on:
* Monday board history: search for related items on the tasks board
* System doc content: extract more context from the "Known Issues", "Architecture", and "Key Entry Points" sections
* The goal is the same: exhaust available context before asking the user

### 3b. Git history (engineering/data teams only)

Skip this step if the system doc has no `Repos` section.

On the relevant files, run:
```bash
git -C <repo-path> log --oneline -20 -- <relevant-file-paths>
```
Use commit messages to understand what has changed recently. Translate into product context (e.g. "a new creation wizard was recently introduced"), not commit hashes.

### 3c. Slack
Search the relevant system channel and the team channel (from `references/slack.md`) for recent discussions about the task topic. Use Slack search with keywords from the task name.

This surfaces product decisions, user feedback, and open debates that aren't in code or Monday.

---

## Step 4: Section Walkthrough

Walk through each section with the user - one at a time. Don't dump a full draft upfront. For each section:
1. Share your read based on context
2. Ask if it's right and if anything is missing
3. Wait for confirmation or correction before moving on

Do this for **Why**, then **What**, then **Done When** - in that order.

Keep each message short. One section at a time. Use casual language throughout.

Example flow:

```
**Why - here's my read:**
[1-2 sentences from your research]

Sound right, or is there a different pain point driving this?
```

Wait for response, then:

```
**What - here's my read:**
[1-3 sentences on what changes]

Anything missing or different from what you had in mind?
```

Wait for response, then:

```
**Done When - draft:**
- [ ] [scenario]
- [ ] [scenario]
- [ ] [scenario]

Anything missing or wrong here?
```

Once all three sections are confirmed, move to Step 5 (write to Monday). Do NOT ask the user to confirm again - just write it.

---

## Step 5: Draft the Final Brief

Assemble the confirmed sections into the final brief. No need to show it again - go straight to writing to Monday.

---

## Step 6: Task Metadata (new items only, run in parallel with Step 4)

Skip if updating an existing item.

1. Select the board from `references/monday_boards.md` (default: the team tasks board; use a different board only if the matched system documents one).
2. Read `references/monday_boards.md` for board IDs and known column keys.
3. Ask ALL of the following in a single question batch:

**Board** (default inferred from system):
- Team tasks board (default)
- Other boards documented in `references/monday_boards.md`

**Planning bucket** (adapt to how the board is organized - sprints, weekly groups, or none):
- This week / current sprint
- This month / quarter
- Backlog
- Unplanned urgent

**Owner** (default = me):
- Me (default)
- Unassigned
- Someone else

**Priority** (default = Medium):
- Medium
- High
- Critical
- Best Effort

**System / Area** (optional - reads from the Systems Reference table in CLAUDE.md):
- Other / None

4. If owner = "Someone else": follow up with `list_users_and_teams` to look up their ID.
5. If owner = "Me": resolve the current user ID at write time via `get_user_context`.

Only set system, priority, type, and owner columns when the exact monday column keys or label IDs are documented in `references/monday_boards.md`. If they are not documented, omit those fields and report the missing schema after item creation.

---

## Step 7: Write to Monday

**Task name (new items):** Generate a short, human-sounding name - 5-8 words max, lowercase except proper nouns. Infer it from the description; do NOT ask the user. Examples: `"fix widget sync failures"`, `"add metadata filters to API"`, `"move token generation outside settings page"`.

**New item** - call `create_item`:
* `boardId`: selected board ID from Step 6
* `name`: inferred short task name (see above)
* `columnValues`: only set fields whose column keys are documented in `references/monday_boards.md`. Two gotchas that apply on every monday board:
  * Status/priority/type columns take `{"label": "..."}` - the label must exist on the board, so use the exact labels documented in `references/monday_boards.md`.
  * Person columns take `{"personsAndTeams": [{"id": OWNER_ID, "kind": "person"}]}` where `OWNER_ID` is the numeric user ID resolved in Step 6 (omit the whole key if Unassigned). The `person-<id>` string form is for **filters only** - passing it to `create_item` fails with "User with email = person-... was not found".

If required column keys are not documented, create the item with title and description only, then report which metadata could not be set.

**Existing item** - use the existing item ID. No column changes needed.

**Set the description** via `all_monday_api`. Pass the markdown as a GraphQL **variable**, not interpolated into the query string - the brief contains quotes, backslashes, and newlines that break an inline string literal:

```graphql
mutation SetDesc($itemId: ID!, $markdown: String!) {
  set_item_description_content(item_id: $itemId, markdown: $markdown) {
    success
    error
    block_ids
  }
}
```

Set `variables` to an object whose `itemId` is the created/target item's id and whose `markdown` is the assembled brief - both resolved at runtime, not literal strings (the JSON encoder handles all escaping). **Check `success` in the response before telling the user the description was set; if it is `false`, surface `error` instead of reporting success.**

> **Known monday platform failure:** `set_item_description_content` can return `INTERNAL_SERVER_ERROR` even with trivial content (and even with the markdown passed as a variable, so it is not an escaping problem) in at least two situations:
> - **Items just created via the API** - the item's description document does not exist yet, and `create_doc` cannot initialize it (it only supports board/workspace locations).
> - **monday CRM-product boards.**
>
> **Fallback:** post the same brief as the item's first update via `create_update`, which takes an **HTML** body (not markdown), then tell the user it landed in the item's updates instead of the description. Convert the Why/What/Done When/Open Questions template to HTML first - this is not optional, markdown passed to `create_update` renders as literal text:
> - Headings `## Why` → `<h2>Why</h2>`
> - Bullets/checkboxes `- [ ] scenario` → `<ul><li>scenario</li></ul>`
> - Paragraphs → `<p>...</p>`, italics `*x*` → `<em>x</em>`
>
> Pass the HTML as the `body` argument (the `create_update` tool accepts it directly, so no query-string escaping problem). Tell the user it landed in the updates only after `create_update` returns an `id`; if it does not, surface the failure instead of reporting success. Retry the `set_item_description_content` mutation only if the user asks.

Template:

```markdown
## Why
{1-2 sentences max}

## What
{1-3 sentences max}

## Done When
- [ ] {scenario in plain language}
- [ ] {scenario}
- [ ] {scenario - 2-4 max}

## Open Questions
- {one line per question}
(omit if none)

---
*Documented via Claude Code on {today's date}*
```

---

## Step 8: Confirm

Return the item URL: `https://{{MONDAY_WORKSPACE}}.monday.com/boards/{board_id}/pulses/{item_id}`

---

## Key Principles

* **Exhaust context before asking.** Monday, epic, siblings, system doc, code, git history, Slack - use all of it. The user should only fill what you genuinely can't find.
* **This is a product skill, not an engineering skill.** Read the code to understand what users experience today. Never surface file names, function names, component names, or technical internals in the brief. Translate everything into user-facing, business-facing language.
* **One output format, always.** Why / What / Done When / Open Questions. Nothing else.
* **Section walkthrough, not a full draft.** Walk through Why, What, Done When one at a time. Share your read, confirm with the user, then move on. Write to Monday only after all three are confirmed.
* **Casual tone, plain words.** Write like a teammate, not a spec writer. "Clean up" not "purge", "pick" not "configure". Short sentences.
* **Done When = checklist, not BDD.** Use `- [ ]` format. Plain language scenarios, no "Given/When/Then".
* **Batch questions, not drip questions.** Ask everything at once.
