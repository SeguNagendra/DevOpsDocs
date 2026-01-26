---
sidebar_position: 2
---

# Advanced Metrics Concepts

> *“At scale, most observability problems are metrics problems.”*

This module belongs to **PHASE 5: Metrics (Time-Series Data)**.  
Here we focus on **how metrics behave at scale**, how queries work, and how metrics directly impact **alert quality and cost**.

---

## Percentiles (Why Averages Lie)

Percentiles describe distributions, not averages.

Common percentiles:
- p50 → median
- p95 → worst experience for 5% of users
- p99 → tail latency

Best practice:
> Use p95 or p99 for user-facing latency.

---

## Distribution Metrics Revisited

Distribution metrics:
- Enable accurate percentiles
- Are essential for latency analysis

Use distributions for:
- APIs
- Databases
- Queues

---

## Metric Queries (Conceptual)

A metric query defines:
- Metric name
- Tags
- Aggregation
- Time window

Example:
```
avg:http.request.latency{env:prod,service:checkout}
```

Queries turn raw data into insight.

---

## Aggregation Across Dimensions

Metrics can be aggregated:
- Across hosts
- Across services
- Across regions

Wrong aggregation can:
- Hide failures
- Create false confidence

---

## Rollups & Resolution

Metrics are stored at different resolutions.

Rollups:
- Aggregate older data
- Reduce storage cost
- Improve performance

High resolution:
- Recent data

Low resolution:
- Historical data

---

## Cardinality (Deep Dive)

Cardinality is the number of **unique tag combinations**.

High cardinality:
- Increases cost
- Slows queries
- Impacts limits

Never use:
- user_id
- request_id
- session_id

Golden rule:
> Cardinality must be bounded and predictable.

---

## Metrics & Cost Relationship

Cost drivers:
- Number of custom metrics
- Cardinality
- High-resolution data

Cost control starts with:
> Good metric design.

---

## Metrics & Alert Quality

Bad metrics cause:
- Alert fatigue
- Missed incidents

Good metrics enable:
- Stable alerts
- Clear thresholds
- SLO-based alerting

---

## Common Advanced Mistakes

❌ Alerting on averages  
❌ Ignoring cardinality  
❌ Over-collecting metrics  
❌ No metric lifecycle management  

---

## Key Takeaways

- Percentiles show real experience
- Cardinality is the biggest risk
- Aggregation choices matter
- Metrics directly impact cost and alerts

---

➡️ **Next Phase:** Events, Changes & Context
