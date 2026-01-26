---
sidebar_position: 2
---

# Cost Optimization Strategies

> *“Good observability shows everything. Great observability shows only what matters.”*

This module belongs to **PHASE 14: Cost Management & Optimization**.  
Here we focus on **practical, real-world strategies** to keep Datadog costs under control **without losing visibility**.

---

## Cost Optimization Is a Design Problem

Most cost issues come from:
- Poor tagging decisions
- High-cardinality data
- Collecting data nobody uses

Cost optimization starts with:
> Better design, not panic cleanup.

---

## Metrics Cost Optimization

### Reduce Cardinality

Avoid:
- IDs as tags
- Unbounded values

Prefer:
- Aggregated dimensions
- Stable tags

Rule:
> Fewer unique tag combinations = lower cost.

---

### Review Custom Metrics

Ask:
- Who uses this metric?
- Is it alerting or dashboard-only?
- Can it be aggregated?

Remove:
- Unused metrics
- Duplicates

---

## Logs Cost Optimization

### Index Selectively

Do not index:
- Debug logs
- High-volume info logs

Index:
- Errors
- Security events
- Critical business logs

Remember:
> Indexed logs drive cost.

---

### Archive Everything Else

Archives:
- Cost far less
- Preserve compliance
- Allow rehydration

Strategy:
> Index small, archive large.

---

## APM Cost Optimization

### Tune Sampling

- Reduce sampling for low-value services
- Increase sampling for critical paths

Goal:
> Keep representative traces, not all traces.

---

### Limit Instrumentation

Avoid:
- Tracing internal helper functions
- Instrumenting everything blindly

---

## RUM Cost Optimization

RUM grows with:
- User traffic
- Session volume

Strategies:
- Sample sessions
- Track only key pages
- Exclude bots and internal users

---

## Synthetics Cost Optimization

Synthetic costs depend on:
- Number of tests
- Frequency
- Locations

Optimize by:
- Reducing frequency where possible
- Limiting locations
- Focusing on critical journeys

---

## Governance & Ownership

Cost control requires:
- Ownership
- Review cadence
- Shared responsibility

Best practices:
- Assign team ownership via tags
- Review usage monthly
- Educate teams

---

## Monitor Datadog with Datadog

Use:
- Usage dashboards
- Cost trends
- Anomaly detection on usage

This enables:
> Early detection of runaway costs.

---

## Common Cost Optimization Mistakes

❌ Cutting visibility blindly  
❌ One-time cleanup without process  
❌ No ownership  
❌ Ignoring growth patterns  

---

## Why This Module Matters

Without cost optimization:
- Observability becomes unsustainable
- Teams lose trust

With cost optimization:
- Visibility scales safely
- Datadog remains valuable long-term

---

## Key Takeaways

- Cost is driven by data design
- Cardinality control is critical
- Index selectively, archive broadly
- Sampling balances cost and insight
- Governance sustains optimization

---

➡️ **Next Phase:** Advanced Datadog Practices & Architecture
