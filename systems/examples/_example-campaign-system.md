<!-- last-reviewed: 2026-04-01 -->
<!-- EXAMPLE: Delete this file once you have real system docs -->
# Campaign Operations

> Operating system for planning, launching, and measuring integrated campaigns across channels.

## Overview

Campaign Operations coordinates the work that turns a marketing idea into a launch: brief, audience, message, channel plan, assets, approvals, launch date, and post-launch readout. It is the spine for cross-functional campaigns that touch product marketing, content, lifecycle, paid, website, sales, and analytics.

## How Claude Works With This

| Action | How |
|--------|-----|
| Make changes | Create or update campaign tasks on the Campaign Calendar and Marketing Tasks boards |
| Investigate | Check campaign brief, launch board, Slack launch thread, and reporting dashboard |
| Publish / launch | Follow the launch checklist and confirm owner approvals before sending or scheduling |

## Platforms / Data Sources

| Source | What it contains | Owner |
|--------|------------------|-------|
| monday Campaign Calendar | Launch dates, owners, status, campaign rows | Marketing Ops |
| monday Marketing Tasks | Execution tasks and blockers | Channel owners |
| Google Drive Campaign Folder | Briefs, assets, copy docs, enablement materials | Campaign owner |
| Slack `#campaign-launches` | Day-of coordination and open decisions | Marketing Ops |

## Operating Model

- Campaign owner is accountable for brief quality, launch date, stakeholder signoff, and readout.
- Channel owners own execution details for email, paid, web, content, social, and sales enablement.
- Launch readiness is reviewed two business days before launch.
- Public-facing copy requires brand or product marketing approval before scheduling.

## Key Surfaces

- Campaign brief: audience, problem, offer, message, channels, success metric
- Campaign calendar row: launch date, owner, status, dependency flags
- Launch checklist: assets, tracking, QA, approvals, scheduling, day-of comms
- Reporting view: performance against the campaign's primary metric

## Audience / Segmentation

- Audience source must be named, such as CRM list, product usage segment, customer tier, region, or account list.
- Do not infer audience eligibility from a campaign name alone.
- Suppression rules and consent rules live in the CRM/lifecycle system doc.

## Measurement

| Metric | Source | Notes |
|--------|--------|-------|
| Primary conversion | Campaign dashboard | Must match the brief before launch |
| Channel contribution | UTM reporting view | Requires correct campaign naming |
| Sales follow-up | CRM campaign influence view | Lagging indicator; read after routing completes |

## Known Issues / Failure Modes

| Issue | Symptoms | Resolution |
|-------|----------|------------|
| Brief missing audience or metric | Channel owners ask basic questions late in the process | Send back to campaign owner before execution starts |
| Launch date moves without task updates | Tasks show old due dates and owners miss handoffs | Update campaign row first, then sync downstream task dates |
| Tracking not QAed | Dashboard shows unattributed traffic or broken UTMs | Run tracking QA before scheduling; ask Analytics if naming rules are unclear |

## Related Systems

- **Upstream:** Product launch calendar, customer research, sales priorities
- **Downstream:** CRM/lifecycle, paid acquisition, website/CMS, content calendar, reporting dashboard
- **Partner teams:** Product Marketing, Sales, Design, Data, Web team

## Pointers

- **Skills:** `/marketing-os`, `/pm-story`, `/retro`
- **Boards:** Campaign Calendar, Marketing Tasks
- **Channels:** `#campaign-launches`, `#marketing-announcements`
- **Docs/assets:** Campaign folder template in Drive
