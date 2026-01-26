---
sidebar_position: 1
---

# Monitors & Alerting Fundamentals

> *“Observability without alerting is insight without action.”*

This module belongs to **PHASE 12: Alerting, Reliability & Incident Management**.  
Here we focus on **how Datadog turns signals into actionable alerts**, and how to design alerts that help — not hurt — on-call engineers.

---

## What Is a Monitor?

A **monitor** in Datadog continuously evaluates data and triggers alerts when conditions are met.

Monitors watch:
- Metrics
- Logs
- Traces
- Synthetic tests
- Events

Monitors answer:
> *When should humans be notified?*

---

## Why Alerting Is Hard

Alerting fails when:
- Alerts are too noisy
- Alerts trigger too late
- Alerts lack context

This leads to:
- Alert fatigue
- Ignored notifications
- Slower incident response

Good alerting:
> Notifies the right people, at the right time, with the right context.

---

## Types of Monitors (High Level)

Datadog supports multiple monitor types.

### Metric Monitors
- Based on metric thresholds
- Most common alert type

### Log Monitors
- Trigger on log patterns
- Useful for error detection

### APM Monitors
- Trigger on latency or error rates
- Service-focused

### Synthetic Monitors
- Trigger on test failures
- User-experience focused

---

## Thresholds vs Anomalies

### Threshold-Based Alerts
- Fixed values
- Simple to understand

Example:
- CPU > 80%

### Anomaly-Based Alerts
- Learn normal behavior
- Detect unusual patterns

Best practice:
> Use thresholds for known limits, anomalies for unknown issues.

---

## Alert Severity & States

Monitors usually have states:
- OK
- Warning
- Alert
- No Data

Severity levels help:
- Prioritize response
- Reduce panic

---

## Notification Channels

Alerts can notify via:
- Email
- Chat tools
- Incident platforms

Good notifications include:
- Clear message
- Impact description
- Next steps

---

## Alert Context Is Critical

A good alert answers:
- What is broken?
- Where is it broken?
- How severe is it?
- Who owns it?

Missing context:
> Slows every incident.

---

## Common Alerting Mistakes

❌ Alerting on every metric  
❌ No ownership or routing  
❌ Alerts without runbooks  
❌ Ignoring warning states  

---

## Why This Module Matters

Poor alerting:
- Wakes people unnecessarily
- Hides real incidents

Good alerting:
- Builds trust
- Reduces stress
- Improves reliability

---

## Key Takeaways

- Monitors trigger human action
- Alert quality matters more than quantity
- Context reduces MTTR
- Alerting is part of reliability engineering

---

➡️ **Next Module:** SLOs, SLIs & Error Budgets
