<!-- last-reviewed: 2026-04-01 -->
<!-- EXAMPLE: Delete this file once you have real system docs -->
# Marketing Measurement

> Reporting and attribution layer for campaign performance, channel health, and marketing-sourced impact.

## Overview

Marketing Measurement gives the team a consistent way to read performance across campaigns, channels, website conversion, lifecycle programs, and sourced pipeline. It combines CRM data, web analytics, paid platforms, product signals, and warehouse models into dashboards used for weekly readouts and campaign retros.

## How Claude Works With This

| Action | How |
|--------|-----|
| Make changes | Request dashboard/model updates through Analytics or update owned reporting views if documented |
| Investigate | Check dashboard freshness, source platform numbers, UTM naming, and warehouse job status |
| Publish / launch | Confirm tracking plan before launch; add readout date to campaign tasks |

## Platforms / Data Sources

| Source | What it contains | Owner |
|--------|------------------|-------|
| Looker / Tableau | Marketing dashboards and campaign readouts | Analytics |
| GA4 / web analytics | Traffic, conversion events, landing page behavior | Web / Analytics |
| CRM | Campaign membership, email engagement, lead stages | Marketing Ops |
| Ad platforms | Spend, impressions, clicks, platform conversions | Paid Acquisition |
| Data warehouse | Joined attribution and sourced pipeline models | Data |

## Operating Model

- Weekly marketing readout uses the executive dashboard plus channel-specific caveats.
- Campaign retros use the metric named in the campaign brief, not whatever number looks best.
- Attribution questions should name the model and window before making claims.
- Data freshness issues go to Analytics before performance conclusions are shared.

## Key Surfaces

- Executive marketing dashboard
- Campaign performance dashboard
- Paid channel dashboard
- Website conversion dashboard
- Lifecycle funnel dashboard
- UTM naming reference

## Audience / Segmentation

- Segment definitions must come from the dashboard or data model, not campaign shorthand.
- Account-based and contact-based metrics are not interchangeable.
- Regional, customer/prospect, and lifecycle-stage filters must be named in readouts.

## Measurement

| Metric | Source | Notes |
|--------|--------|-------|
| Marketing-sourced pipeline | Attribution dashboard | Model-dependent and lagging |
| Campaign conversion | Campaign dashboard | Requires clean UTMs and event mapping |
| Channel CAC / spend efficiency | Paid dashboard + finance inputs | Confirm spend window |
| Website conversion rate | Web analytics dashboard | Watch for form and tracking changes |

## Known Issues / Failure Modes

| Issue | Symptoms | Resolution |
|-------|----------|------------|
| Dashboard stale | "Last updated" timestamp is old or metrics are flat | Check warehouse job status and ask Analytics before reporting |
| UTM mismatch | Campaign traffic splits across several names | Map variants to canonical campaign name in the readout and fix naming rules |
| Platform numbers disagree | Ad platform and warehouse conversions differ | Name attribution window and source limitation; do not blend numbers silently |
| Missing campaign ID | CRM influence view omits launched campaign | Confirm campaign member sync and required fields |

## Related Systems

- **Upstream:** CRM, ad platforms, web analytics, product analytics, data warehouse
- **Downstream:** Weekly readout, campaign retros, budget decisions, executive updates
- **Partner teams:** Analytics, Finance, Paid Acquisition, Marketing Ops

## Pointers

- **Skills:** `/marketing-os`, `/retro`
- **Dashboards:** Executive Marketing, Campaign Performance, Paid Efficiency
- **Channels:** `#marketing-analytics`, `#paid-acquisition`
- **Docs/assets:** UTM naming guide, campaign readout template
