<!-- last-reviewed: 2026-04-01 -->
<!-- EXAMPLE: Delete this file once you have real system docs -->
# Product Analytics

> Partner-owned source for product usage, activation, adoption, and customer behavior signals used in marketing audiences and reporting.

## Overview

Product Analytics is owned by Data and Product, but marketing depends on it for audience segmentation, launch targeting, adoption readouts, expansion plays, and lifecycle triggers. When product events lag or definitions change, marketing audiences and campaign reporting can be wrong.

## How Claude Works With This

| Action | How |
|--------|-----|
| Make changes | Marketing does not change product events directly; file a Data/Product Analytics request |
| Investigate | Check product analytics dashboard freshness, event dictionary, and warehouse sync status |
| Escalate | Ask in `#product-analytics` with event name, dashboard link, and campaign impact |

## What Marketing Owns

- Requests for audience definitions and campaign use cases
- Mapping product signals to lifecycle or campaign briefs
- Explaining how a missing or changed event affects marketing work

## What Marketing Does Not Own

- Product event instrumentation
- Warehouse model definitions
- Dashboard permissions and refresh jobs
- Canonical activation/adoption definitions

## When It Breaks

- **Symptoms marketing sees:** audience counts swing unexpectedly, lifecycle triggers stop enrolling, launch readout misses product adoption metrics, or dashboards show stale timestamps.
- **First check:** product analytics dashboard freshness and event dictionary.
- **If it is a data issue:** post in `#product-analytics` with the event, dashboard, timestamp, and business impact.
- **If it is a marketing setup issue:** check CRM list criteria and campaign tracking first.
- **Common false alarm:** new product events may take a day to appear in downstream marketing dashboards.

## Related Systems

- **Upstream:** Product app instrumentation, Segment, warehouse models
- **Downstream:** CRM/lifecycle audiences, campaign measurement, product launch readouts

## Pointers

- **Investment:** Reference Only
- **Owner:** Data / Product Analytics
- **Escalation:** `#product-analytics`
- **Dashboard:** Product Adoption Overview
