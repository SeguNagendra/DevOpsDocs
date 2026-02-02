---
sidebar_position: 3
title: CloudWatch Metrics Deep Dive
---

# CloudWatch Metrics – Deep Dive

Metrics are the **foundation of monitoring**.
To use CloudWatch effectively, you must understand **how metrics are collected, structured, and used for alerting**.

This guide goes beyond basics into **real operational usage**.

---

## Default (AWS) Metrics

AWS services automatically publish metrics.

Examples:
- EC2 → CPUUtilization, NetworkIn
- RDS → CPUUtilization, FreeStorageSpace
- ELB → RequestCount, TargetResponseTime

Key point:
> **You don’t need to install anything for default metrics**

---

## Custom Metrics

Custom metrics are:
- Metrics you publish yourself
- Application or business-level metrics

Examples:
- OrdersPlaced
- LoginFailures
- QueueDepth

Use custom metrics when:
- AWS metrics are not enough
- You need application visibility

---

## Publishing Custom Metrics

Custom metrics are published using:
- CloudWatch API
- AWS SDK
- CloudWatch Agent

Resolution options:
- Standard (1 minute)
- High resolution (1 second)

---

## Metric Resolution (Cost vs Speed)

| Resolution | Use Case |
|---------|----------|
| 1 minute | Normal monitoring |
| 1 second | Latency-sensitive alerts |

High-resolution metrics:
- Cost more
- Should be used selectively

---

## Metric Dimensions (Advanced)

Dimensions:
- Add context
- Create unique metric streams

Example:
- Metric: CPUUtilization
- Dimensions: InstanceId, AutoScalingGroupName

Important rule:
> **Each unique dimension set is a separate metric**

Too many dimensions = higher cost.

---

## Metric Math

Metric math allows:
- Combining metrics
- Creating derived metrics

Examples:
- ErrorRate = Errors / Requests
- CPUAverage across instances

Metric math is powerful for:
- Dashboards
- Complex alarms

---

## Percentiles and Statistics

CloudWatch provides:
- Average
- Minimum
- Maximum
- Sum
- Percentiles (p90, p95, p99)

Best practice:
- Use percentiles for latency
- Avoid averages for user experience

---

## Anomaly Detection

CloudWatch can:
- Learn normal behavior
- Detect anomalies automatically

Used for:
- Unknown failure patterns
- Seasonal traffic

Good for:
- Supplementing threshold-based alarms

---

## Alarming on Metrics (Best Practices)

Alert on:
- Symptoms (high latency)
- Customer impact

Avoid alerting on:
- Root causes directly
- Non-actionable signals

Example:
- Alert on request failures, not CPU alone

---

## Metrics Retention Periods

CloudWatch stores metrics:
- 1 second → 3 hours
- 1 minute → 15 days
- 5 minutes → 63 days
- 1 hour → 15 months

Plan dashboards accordingly.

---

## Common Beginner Mistakes

- Alerting on CPU only
- Too many metrics/dimensions
- Using averages for latency
- No business-level metrics

These mistakes reduce signal quality.

---

## Interview Tip

If asked:
> “How do you monitor applications in AWS?”

Strong answer:
> By using CloudWatch default and custom metrics, percentiles for latency, and alarms on customer-impacting signals.

---

## Key Takeaways

- Metrics are time-series data
- Default and custom metrics complement each other
- Dimensions add power but increase cost
- Percentiles give better insight than averages
- Good metrics lead to good alerts

---

📌 **Next:** CloudWatch Logs Deep Dive
