---
sidebar_position: 1
---

# Dashboards & Widgets

> *“Dashboards don’t just show data — they tell a story.”*

This module belongs to **PHASE 7: Visualization & Analysis**.  
Here we focus on **how to visualize metrics and events in a way that makes problems obvious**, not hidden.

Good dashboards reduce noise.  
Bad dashboards create false confidence.

---

## What Is a Dashboard?

A **dashboard** is a visual representation of system behavior over time.

Dashboards help you:
- Understand system health at a glance
- Spot trends and anomalies
- Share context across teams

Dashboards are:
- For humans, not machines
- For understanding, not raw data dumps

---

## Types of Dashboards in Datadog

Datadog supports different dashboard styles.

### Time-Series Dashboards
- Most commonly used
- Focus on trends over time
- Ideal for monitoring behavior

### Service-Oriented Dashboards
- Focus on a single service
- Combine metrics, events, and logs

Best practice:
> One dashboard per major service or platform area.

---

## What Is a Widget?

A **widget** is a single visualization inside a dashboard.

Widgets answer specific questions:
- How is latency changing?
- Which host is under pressure?
- Are errors increasing?

Dashboards are collections of **well-chosen widgets**.

---

## Common Widget Types

### Time Series
- Line graphs over time
- Best for trends and anomalies

### Query Value
- Single numeric value
- Best for KPIs

### Top List
- Ranked values
- Best for identifying outliers

### Heatmaps
- Distribution over time
- Best for latency analysis

---

## Designing Good Dashboards

Good dashboards:
- Start with key questions
- Show cause before effect
- Use consistent time ranges
- Avoid clutter

Ask yourself:
> *What decision will this dashboard help someone make?*

---

## Using Events on Dashboards

Events add **context** to dashboards.

Examples:
- Deployment markers
- Scaling events
- Configuration changes

Seeing events next to metrics helps:
- Correlate spikes
- Speed up investigation

---

## Audience-Based Dashboards

Different audiences need different dashboards.

Examples:
- Execs → high-level health
- SREs → detailed behavior
- Developers → service performance

Avoid:
> One dashboard trying to serve everyone.

---

## Common Dashboard Mistakes

❌ Too many widgets  
❌ No clear ownership  
❌ Mixing unrelated services  
❌ Using dashboards as alerting tools  

---

## Why This Module Matters

Dashboards are:
- The first thing people check
- The last thing people trust

Poor dashboards:
- Hide real problems
- Delay response

Good dashboards:
- Build confidence
- Speed decisions

---

## Key Takeaways

- Dashboards tell stories
- Widgets answer questions
- Events add context
- Simplicity beats complexity

---

➡️ **Next Module:** Dashboards as Code
