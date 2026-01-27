---
sidebar_position: 2
title: CloudWatch Metrics
---

# CloudWatch Metrics

CloudWatch Metrics are the **foundation of monitoring in AWS**.
They tell you **how your system is behaving over time**.

If logs answer *why something failed*,
👉 **metrics answer whether your system is healthy**.

---

## What Are CloudWatch Metrics?

Metrics are:
- Time-series numerical data
- Collected at regular intervals
- Stored per region

Examples:
- EC2 CPUUtilization
- ALB RequestCount
- Lambda Invocations
- RDS FreeStorageSpace

---

## Why Metrics Matter

Metrics help you:
- Detect performance issues
- Identify scaling needs
- Trigger alarms and automation
- Make capacity decisions

Without metrics:
- You are guessing
- Problems are detected too late

---

## Metric Structure (Must Know)

Every CloudWatch metric has:

- **Namespace**
- **Metric Name**
- **Dimensions**
- **Timestamp**
- **Value**
- **Unit**

Understanding this structure makes CloudWatch easy.

---

## Namespaces

A namespace is:
- A container for related metrics

Examples:
- `AWS/EC2`
- `AWS/ELB`
- `AWS/Lambda`
- Custom namespaces (your app)

👉 Namespaces prevent metric name collisions.

---

## Metric Names

Metric name describes:
- What is being measured

Examples:
- CPUUtilization
- NetworkIn
- RequestCount
- Duration

Metric names **mean nothing without dimensions**.

---

## Dimensions (Very Important)

Dimensions:
- Are key-value pairs
- Identify **what resource** the metric belongs to

Example:
```
InstanceId = i-1234567890
```

Same metric name +
Different dimensions =
Different metric

👉 Dimensions provide granularity.

---

## Resolution and Granularity

### Standard Resolution
- 5-minute intervals
- Default for most services

### High-Resolution Metrics
- 1-second intervals
- Extra cost

Used for:
- Latency-sensitive systems
- Real-time monitoring

---

## Default vs Custom Metrics

### Default Metrics
- Provided automatically
- Infrastructure-level

Examples:
- EC2 CPU
- ELB request count

### Custom Metrics
- Published by you
- Application or business metrics

Examples:
- Orders processed
- Login failures
- Queue depth

---

## Publishing Custom Metrics

Custom metrics can be published using:
- AWS SDK
- AWS CLI
- CloudWatch Agent

Use cases:
- Application health
- Business KPIs

👉 Custom metrics improve observability.

---

## Metric Math

CloudWatch supports:
- Basic calculations
- Aggregations
- Expressions

Examples:
- Error rate
- Average latency
- Percentiles

Metric math enables **advanced monitoring**.

---

## Common Metric Pitfalls

- Monitoring only CPU
- Ignoring memory and disk
- Too many metrics (cost issue)
- No alarms on critical metrics

Monitoring must be:
- Relevant
- Actionable

---

## Interview Tip

If asked:
> “What are CloudWatch metrics?”

Strong answer:
> CloudWatch metrics are time-series data points that represent the performance and health of AWS resources and applications.

---

## Key Takeaways

- Metrics show system health
- Namespaces organize metrics
- Dimensions identify resources
- Custom metrics add visibility
- Foundation for alarms and automation

---

📌 **Next:** CloudWatch Logs
