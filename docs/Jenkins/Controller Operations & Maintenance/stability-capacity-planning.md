---
sidebar_position: 8
---

# Stability & Capacity Planning

Stability and capacity planning ensure Jenkins remains **reliable under growth**.
Most outages happen because capacity planning was ignored until it was too late.

---

## Why Capacity Planning Matters

Without capacity planning:
- Build queues grow uncontrollably
- Controllers become unstable
- Agents thrash or starve
- Cloud costs spike unexpectedly

Stability is a result of planning.

---

## Core Capacity Dimensions

Jenkins capacity depends on:
- Controller resources
- Agent count and size
- Executor configuration
- Job complexity
- Concurrency patterns

Ignoring any dimension leads to failure.

---

## Queue-Based Capacity Planning

Key signals:
- Queue wait time
- Queue length
- Executor utilization

Queues tell the truth about capacity.

---

## Controller Stability Indicators

Watch for:
- UI lag
- Frequent GC pauses
- Thread exhaustion
- Jenkins restarts
- Slow configuration saves

These indicate controller stress.

---

## Agent Capacity Planning

Best practices:
- Prefer many small agents
- One executor per agent
- Scale horizontally
- Separate heavy and light workloads

Avoid oversized agents.

---

## Workload Segmentation

Segment by:
- Team
- Environment (prod vs non-prod)
- Trust level
- Resource intensity

Segmentation improves stability.

---

## Growth Forecasting

Plan for:
- New teams onboarding
- Increased build frequency
- Heavier pipelines
- Additional integrations

Capacity planning must be forward-looking.

---

## Cost vs Stability Trade-offs

- Over-provisioning = wasted cost
- Under-provisioning = outages

Aim for controlled headroom.

---

## Capacity Review Cadence

Recommended:
- Monthly capacity review
- Quarterly scaling adjustments
- Post-incident capacity reassessment

Capacity planning is continuous.

---

## Common Capacity Planning Failures

- Reactive scaling only
- No queue monitoring
- Single shared agent pool
- No separation of workloads

---

## Best Practices

- Monitor queue metrics
- Scale agents dynamically
- Keep controller lean
- Document capacity assumptions

---

## Interview Focus Areas

- Queue-driven scaling
- One executor per agent rationale
- Capacity vs performance trade-offs

