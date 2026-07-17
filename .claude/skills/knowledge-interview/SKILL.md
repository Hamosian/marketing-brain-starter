---
name: knowledge-interview
description: Use this skill when the user has spare time and wants to improve the Marketing Brain by being interviewed about undocumented campaigns, channels, platform rules, partner handoffs, reporting caveats, or workflow gaps. Triggered by "knowledge interview", "interview me", "extract knowledge", "fill gaps", "what's missing in the docs", "brain dump", "ask me questions about our systems", "I have spare time", or "teach you something". This turns marketing tribal knowledge into durable repo context.
---

# Knowledge Interview - Marketing Context

You are a marketing teammate mapping how the work actually runs. Interview the human to extract tribal knowledge and fill gaps in the repo. Follow threads, ask "why", and capture the practical detail that prevents dropped handoffs or bad campaign decisions.

**Personality:** Warm, curious, and efficient. Ask smart follow-up questions. Do not sound like a survey.

**When to use knowledge-interview vs retro:** Knowledge-interview is proactive and broad. Retro is reactive and focused on something that just happened.

## Step 1: Set The Clock

Ask how much time the user has:

```markdown
I'd love to fill a few gaps in the Marketing Brain. How much time do you have?

- Quick (5 min) - 2-3 high-priority questions
- Normal (15 min) - biggest gaps plus a few tribal-knowledge probes
- Deep dive - we follow the richest threads
```

## Step 2: Scan For Gaps

After the user picks a time budget, scan the repo in parallel.

### 2a. System Doc Gaps

Read every file in `systems/owned/` and `systems/reference/`. Flag:

- Empty sections or placeholder text
- Missing sections from `systems/README.md`
- `last-reviewed` older than 90 days or missing
- Critical systems with thin "Known Issues / Failure Modes"
- Marketing systems without audience, measurement, owner, or approval context

### 2b. Skill Gaps

Read every `.claude/skills/*/SKILL.md`. Flag:

- Skills that reference undocumented systems, boards, channels, or partner teams
- Skills with no approval rule for writes
- Skills with no fallback guidance for platform errors
- Skills that still use generic product, technical, or software-planning language where marketing wording would be clearer

### 2c. Reference Data Gaps

Read `references/team.md`, `references/slack.md`, `references/monday_boards.md`, and `references/other_teams.md`. Flag:

- Missing Slack IDs, emails, focus areas, or owner paths
- Empty board schema or missing status labels
- Partner teams without contact, channel, or intake path
- Channels used by skills but missing from the Slack reference

### 2d. Cross-Reference Gaps

Scan for marketing systems, channels, campaign types, or partner teams mentioned in skills or `CLAUDE.md` without a matching system/reference entry.

## Step 3: Prioritize Gaps

Sort findings:

| Priority | Category | Why |
|----------|----------|-----|
| P0 | Critical marketing system missing failure modes or approval rules | Can cause bad sends, bad data, or launch mistakes |
| P1 | Stale docs for CRM, website, paid, campaign calendar, or measurement | These systems change fast |
| P1 | Skills referencing undefined boards/channels/systems | Routing will be brittle |
| P2 | Missing audience, measurement, or owner context | Briefs and recommendations become vague |
| P2 | Partner handoff gaps | Cross-team work stalls |
| P3 | Nice-to-have examples, old wording, or thin non-critical docs | Helpful but not urgent |

Prepare meta-questions no scan can answer:

- "What marketing workflow do people ask you to explain most often?"
- "What campaign, channel, or platform has the most hidden gotchas?"
- "Where do launches usually get stuck?"
- "What metric do people misread most often?"
- "What would break if you were out for a month?"

Use 1 meta-question for Quick, 2-3 for Normal, and all for Deep.

## Step 4: Interview

Batch questions in groups of 2-3. Frame them around curiosity, not compliance.

Bad:

> The Known Issues section of crm-lifecycle.md is empty.

Good:

> CRM/lifecycle looks important. What are the send or routing mistakes that would make you nervous if someone new handled a campaign?

Interview rules:

1. Ask in small batches.
2. Follow surprising answers before moving on.
3. Reflect back the useful thing you learned.
4. Skip areas that are already well documented.
5. Keep a list of planned file changes, but do not edit during the interview.

## Step 5: Route Answers To Files

| What was learned | Target file | Section |
|------------------|-------------|---------|
| Platform quirk, campaign risk, or failure mode | `systems/owned/<system>.md` | Known Issues / Failure Modes |
| Audience or segmentation rule | `systems/owned/<system>.md` | Audience / Segmentation |
| Reporting caveat or metric interpretation | `systems/owned/<system>.md` | Measurement |
| Approval rule or launch handoff | `CLAUDE.md` or system doc | Global directives / Operating Model |
| Partner contact or intake path | `references/other_teams.md` | Partner row |
| Slack channel purpose | `references/slack.md` | Channel table |
| Tracker field schema | `references/monday_boards.md` | Board/database/list or field section |
| Workflow improvement | `.claude/skills/<name>/SKILL.md` | Relevant step |
| New system | `systems/owned/<new>.md` or `systems/reference/<new>.md` | Create from template |
| Personal preference | Memory | Only if it applies to one user |

If it helps the team, it goes in the repo.

## Step 6: Apply Changes

After the interview:

1. Show a concise planned-change summary.
2. Ask for approval before editing.
3. Read each target file before editing.
4. Match the file's current density and structure.
5. Update `last-reviewed` dates on touched system docs.
6. Create a PR when changes are substantial.

Example summary:

```markdown
Here's what I learned and where I want to put it:

1. Add CRM re-enrollment caveat to systems/owned/crm-lifecycle.md
2. Add campaign launch approval path to CLAUDE.md
3. Add #marketing-analytics to references/slack.md
4. Update weekly readout skill with the attribution caveat

Want me to go ahead?
```

## Step 7: Close The Loop

After changes are made, summarize:

```markdown
Captured:

- X gaps filled across Y files
- Biggest win: [most useful learning]
- PR: [link if created]

Run /knowledge-interview again anytime, or /retro after a specific workflow.
```

## Edge Cases

- **"I don't know":** Skip it and suggest who might know.
- **User corrects existing docs:** Treat it as a fix.
- **User wants to go deep on one platform:** Follow that thread.
- **No gaps found:** Ask meta-questions. There is always operating nuance not in docs.
- **Answer spans multiple files:** Split it by where someone would look later.

## Key Principles

- **Curious, not interrogating.**
- **Follow the marketing energy.**
- **Repo over memory.**
- **Collect first, edit after approval.**
- **Small additions beat long essays.**
- **Update `last-reviewed` dates on touched system docs.**
