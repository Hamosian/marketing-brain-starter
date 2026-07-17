# Marketing Systems Directory

## What Is a Marketing System?

A **marketing system** is any platform, workflow, dataset, channel, or operating surface the team uses to plan, launch, measure, or improve go-to-market work.

Examples:

| Area | Owned systems | Reference systems |
|------|---------------|-------------------|
| CRM and lifecycle | HubSpot, Marketo, nurture programs, scoring rules | Sales CRM, product usage data |
| Website and conversion | CMS, landing pages, CRO backlog, forms | Web team, brand library |
| Paid acquisition | Google Ads, Meta, LinkedIn, budget tracker | Finance budget system, attribution dashboards |
| Content and SEO | Content calendar, blog CMS, SEO tracker | Product roadmap, brand guidelines |
| Campaign operations | Campaign calendar, launch checklist, partner handoffs | Product launch calendar, design intake |
| Measurement | Marketing dashboards, attribution model, reporting cadence | Data warehouse, analytics platform |

Split docs into two categories:

- **`owned/`** - systems marketing owns or operates directly
- **`reference/`** - systems marketing depends on but another team owns

These are **operating maps, not full manuals**. Add enough context for Claude to route work, ask better questions, avoid common mistakes, and find the live source.

## Owned Systems

Systems the marketing team owns, configures, operates, or is accountable for.

<!-- Populated during /setup and as you document more. Examples: -->
<!-- | System | Criticality | Notes | -->
<!-- |--------|-------------|-------| -->
<!-- | [CRM and Lifecycle](owned/crm-lifecycle.md) | Critical | Segments, nurtures, scoring, automations | -->
<!-- | [Marketing Website](owned/marketing-website.md) | High | Landing pages, forms, CRO, CMS publishing | -->
<!-- | [Paid Acquisition](owned/paid-acquisition.md) | High | Channel accounts, campaigns, budget rules | -->
<!-- | [Campaign Calendar](owned/campaign-calendar.md) | High | Launch dates, owners, milestones, partner handoffs | -->
<!-- | [Content Operations](owned/content-operations.md) | Medium | Editorial calendar, publishing workflow, SEO refreshes | -->

| System | Criticality | Notes |
|--------|-------------|-------|

## Reference Systems

Systems marketing depends on but does not own.

<!-- Add systems you depend on. Example: -->
<!-- | System | Owner | Why it matters | -->
<!-- |--------|-------|----------------| -->
<!-- | [Product Analytics](reference/product-analytics.md) | Data | Activation, usage, adoption, audience signals | -->
<!-- | [Brand Library](reference/brand-library.md) | Design | Creative assets, logo usage, visual QA | -->
<!-- | [Sales CRM](reference/sales-crm.md) | Sales Ops | Lead routing, opportunity stages, source attribution | -->

## Templates

Every system doc must include a `<!-- last-reviewed: YYYY-MM-DD -->` comment on the **first line of the file** before the title. `/health-check` uses this to flag stale context.

### Full Template (Active Marketing System)

Use for systems with active execution, high business impact, significant risk, or frequent cross-team handoffs.

```markdown
<!-- last-reviewed: 2026-03-31 -->
# System Name

> One-line description of what this system helps marketing do.

## Overview
What this system does, who uses it, and why it matters to marketing outcomes.

## How Claude Works With This
| Action | How |
|--------|-----|
| Make changes | Platform/admin path, monday board, Notion database, ClickUp list, CMS, CRM, or skill |
| Investigate | Dashboard, report, Slack channel, query, or owner |
| Publish / launch | Approval path, scheduler, or handoff owner |

## Platforms / Data Sources
| Source | What it contains | Owner |
|--------|------------------|-------|
| Platform or view | Brief description | Team/person |

## Operating Model
- Who owns day-to-day operation
- Who approves changes
- How work enters the system
- What cadence or launch rhythm matters

## Key Surfaces
- Main views, boards, campaigns, automations, reports, or pages
- Where configuration lives
- Where to look first when something is off

## Audience / Segmentation
- Primary audiences, lists, segments, territories, or traffic sources
- Any rules Claude must not guess

## Measurement
| Metric | Source | Notes |
|--------|--------|-------|
| Metric name | Dashboard/report | Caveat or owner |

## Known Issues / Failure Modes
| Issue | Symptoms | Resolution |
|-------|----------|------------|
| Description | What marketers see | What to do or who to ask |

## Related Systems
- **Upstream:** what feeds this system
- **Downstream:** what depends on it
- **Partner teams:** who needs to be involved

## Pointers
- **Skills:** relevant skills in this repo
- **Dashboards:** links to live reporting
- **Tracker:** monday boards, Notion databases, ClickUp lists, or planning groups/views
- **Channels:** Slack channels for questions or alerts
- **Docs/assets:** source-of-truth folders or docs
```

### Light Template (Reference Or Partner-Owned System)

Use for systems marketing relies on but does not own. Keep it short and focused on what Claude needs to know to route work correctly.

```markdown
<!-- last-reviewed: 2026-03-31 -->
# System Name

> One-line description of why marketing cares.

## Overview
What the system does and how marketing uses it.

## How Claude Works With This
| Action | How |
|--------|-----|
| Make changes | We do not, or approved handoff path |
| Investigate | Read-only dashboard, owner, or channel |
| Escalate | Partner team, intake form, or Slack channel |

## What Marketing Owns
- The parts marketing can change or request

## What Marketing Does Not Own
- The parts owned by another team

## When It Breaks
- Symptoms marketing sees
- First place to check
- Who to escalate to

## Related Systems
- **Upstream:** what feeds this system
- **Downstream:** what depends on this system

## Pointers
- Investment: Reference Only
- Owner: team/person
- Escalation: team/channel/intake path
```

### Compliance Checklist

Before merging a system doc PR, verify:

- [ ] First line is `<!-- last-reviewed: YYYY-MM-DD -->`
- [ ] The doc uses the full or light template appropriately
- [ ] "How Claude Works With This" explains make changes, investigate, and publish/escalate
- [ ] No TODO or placeholder comments remain in live docs
- [ ] Pointers include real links or named owners
- [ ] Related Systems lists upstream, downstream, and partner dependencies where relevant
- [ ] Measurement caveats are documented when performance numbers are involved

## Examples

See:

- `systems/examples/_example-campaign-system.md` for campaign operations
- `systems/examples/_example-lifecycle-crm-system.md` for CRM and lifecycle
- `systems/examples/_example-marketing-measurement-system.md` for reporting and attribution
- `systems/examples/_example-product-analytics-dependency.md` for a partner-owned dependency
