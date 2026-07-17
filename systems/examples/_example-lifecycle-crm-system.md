<!-- last-reviewed: 2026-04-01 -->
<!-- EXAMPLE: Delete this file once you have real system docs -->
# CRM and Lifecycle

> Owns audience lists, nurture flows, lead routing, email programs, and lifecycle automation.

## Overview

The CRM and Lifecycle system is where marketing turns audience intent into targeted follow-up. It manages forms, lists, segments, scoring, email programs, nurture flows, handoff rules, and campaign attribution fields. Lifecycle, demand generation, sales, and analytics all rely on it staying clean.

## How Claude Works With This

| Action | How |
|--------|-----|
| Make changes | Draft the change request, then confirm before updating CRM workflows, lists, forms, or emails |
| Investigate | Check campaign membership, list rules, workflow history, form submissions, and CRM sync status |
| Publish / launch | Schedule or activate only after owner approval, QA send, suppression check, and tracking check |

## Platforms / Data Sources

| Source | What it contains | Owner |
|--------|------------------|-------|
| HubSpot / Marketo | Lists, forms, emails, workflows, scoring | Lifecycle Marketing |
| Salesforce | Leads, contacts, accounts, opportunities, routing status | Sales Ops |
| Data warehouse | Product usage, account traits, enrichment fields | Data |
| monday Marketing Tasks | Requested lifecycle changes and campaign tasks | Marketing Ops |

## Operating Model

- Lifecycle owner approves automation changes and email sends.
- Sales Ops approves changes that affect lead routing, MQL definitions, or handoff fields.
- Every audience build needs inclusion rules, suppression rules, consent basis, and owner signoff.
- Every send needs QA for copy, links, personalization, UTM tags, and audience count.

## Key Surfaces

- Active nurture programs and enrollment criteria
- Campaign lists and suppression lists
- Lead scoring and MQL routing rules
- Form and landing page integrations
- Email performance and deliverability dashboards

## Audience / Segmentation

- Never guess audience eligibility. Read the list or workflow rules.
- Suppress customers, competitors, unsubscribed contacts, internal domains, and region-specific exclusions when relevant.
- If product usage data is part of the audience, confirm refresh cadence and last successful sync.

## Measurement

| Metric | Source | Notes |
|--------|--------|-------|
| Delivered / opened / clicked | CRM email performance | Useful for channel health, not final business impact |
| MQLs / routed leads | CRM lifecycle dashboard | Confirm routing lag before reporting |
| Pipeline influence | Salesforce or attribution dashboard | Usually lagging and model-dependent |
| Unsubscribe / spam rate | CRM deliverability view | Must be checked after large sends |

## Known Issues / Failure Modes

| Issue | Symptoms | Resolution |
|-------|----------|------------|
| Stale product usage segment | Audience count looks too low or too high | Check warehouse sync timestamp and ask Data if refresh failed |
| Workflow re-enrollment surprise | Contacts receive a message twice | Check re-enrollment rules before activation |
| Broken personalization token | Test email shows blank or fallback copy | Verify token exists for the target object and add fallback copy |
| Lead routing delay | New MQLs sit without owner | Check CRM-to-Salesforce sync and routing workflow history |

## Related Systems

- **Upstream:** Website forms, product usage data, enrichment provider, campaign briefs
- **Downstream:** Salesforce, sales alerts, campaign reporting, customer communications
- **Partner teams:** Sales Ops, Data, Product Marketing

## Pointers

- **Skills:** `/marketing-os`, `/pm-story`, `/retro`
- **Dashboards:** Lifecycle Performance, Deliverability, Lead Routing
- **Boards:** Marketing Tasks, Campaign Calendar
- **Channels:** `#lifecycle-marketing`, `#sales-ops`
