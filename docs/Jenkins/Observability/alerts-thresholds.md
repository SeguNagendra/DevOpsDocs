---
sidebar_position: 4
---

# Alerts & Thresholds

Alerts decide **when humans should intervene**.
Poor alerting causes either missed incidents or constant noise.

---

## Why Alerting Matters

Without alerts:
- Incidents are discovered by users
- SLAs are violated silently
- Small issues become outages

Too many alerts are equally dangerous.

---

## Alerts vs Metrics

- Metrics show trends
- Alerts demand action

Every alert should be **actionable**.

---

## Alert Design Principles

Good alerts are:
- Actionable
- Specific
- Timely
- Rare

If an alert doesn’t require action, remove it.

---

## Critical Jenkins Alerts

Must-have alerts:
- Jenkins controller down
- Queue wait time exceeds threshold
- No available agents
- Authentication failures spike
- Disk almost full

These indicate real impact.

---

## Warning-Level Alerts

Useful warnings:
- Increasing queue length
- Rising build failure rate
- High JVM memory usage
- Agent startup delays

Warnings allow proactive fixes.

---

## Threshold Selection

Thresholds should be:
- Based on baselines
- Tuned over time
- Different for prod vs non-prod

Avoid static, arbitrary thresholds.

---

## Alert Routing

Best practices:
- Route alerts to correct team
- Use escalation policies
- Separate infra vs pipeline alerts

Avoid alert confusion.

---

## Alert Fatigue Prevention

Techniques:
- Alert on symptoms, not causes
- Aggregate related alerts
- Suppress during maintenance

Noise kills alert effectiveness.

---

## Testing Alerts

Always:
- Test alerts periodically
- Verify delivery channels
- Confirm runbooks exist

Untested alerts will fail.

---

## Common Alerting Failures

- Alerting on every metric
- No ownership defined
- No runbooks
- Ignoring alert history

---

## Best Practices

- Start with few critical alerts
- Add warnings gradually
- Review alerts quarterly
- Tie alerts to SLOs

---

## Interview Focus Areas

- What makes a good alert
- Difference between alerts and monitoring
- Queue-based alerting importance

