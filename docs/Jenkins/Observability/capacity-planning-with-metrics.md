---
sidebar_position: 6
---

# Capacity Planning with Metrics

Capacity planning with metrics ensures Jenkins **scales predictably** instead of reacting to outages.
Metrics turn capacity planning from guesswork into engineering.

---

## Why Metrics-Driven Capacity Planning Matters

Without metrics:
- Scaling decisions are reactive
- Costs grow unexpectedly
- Performance degrades silently
- Teams argue with opinions, not data

Metrics provide objective signals.

---

## Core Metrics for Capacity Planning

Focus on these metrics:
- Queue wait time (primary signal)
- Queue length
- Executor utilization
- Agent startup latency
- Build throughput
- Failure and retry rates

Queue metrics matter most.

---

## Establishing Baselines

Steps:
1. Observe normal operating conditions
2. Capture average and peak values
3. Define acceptable ranges
4. Revisit after changes

Baselines anchor decisions.

---

## Identifying Saturation Points

Look for:
- Rapidly increasing queue time
- High executor utilization with idle controller
- Agent startup delays
- Build time variance spikes

These indicate capacity limits.

---

## Scaling Decisions Based on Metrics

Examples:
- High queue time → add agents
- High agent startup time → warm pools or images
- High retry rate → fix instability before scaling

Scale the right layer.

---

## Short-Term vs Long-Term Planning

- Short-term: burst traffic, incidents
- Long-term: team growth, new pipelines

Both require different responses.

---

## Cost-Aware Capacity Planning

Balance:
- Performance SLAs
- Infrastructure cost
- Idle capacity risk

Use headroom, not over-provisioning.

---

## Forecasting Growth

Forecast using:
- Historical queue trends
- Team onboarding plans
- Pipeline complexity changes

Capacity planning should be proactive.

---

## Review & Feedback Loop

Recommended cadence:
- Weekly review during growth
- Monthly steady-state review
- Post-incident reassessment

Planning is continuous.

---

## Common Capacity Planning Mistakes

- Scaling only on CPU
- Ignoring queue metrics
- No baselines
- Overreacting to spikes

---

## Best Practices

- Let queue metrics drive scaling
- Review trends, not snapshots
- Separate capacity and performance issues
- Document scaling assumptions

---

## Interview Focus Areas

- Why queue time is the best signal
- Metrics vs intuition in scaling
- Cost vs capacity trade-offs

