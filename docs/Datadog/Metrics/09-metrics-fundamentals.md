---
sidebar_position: 1
---

# Metrics Fundamentals

> *“If you understand metrics, you understand Datadog.”*

This module belongs to **PHASE 5: Metrics (Time-Series Data)**.  
Metrics are the **foundation of dashboards, alerts, and SLOs** in Datadog.

Before logs, traces, or advanced analytics, teams must clearly understand **what metrics are, how they behave, and how they should be designed**.

---

## What Is a Metric?

A **metric** is a numeric measurement collected over time.

Every metric has:
- A **name**
- A **value**
- A **timestamp**
- A set of **tags**

Metrics answer:
> *How is something behaving over time?*

---

## Why Metrics Are So Important

Metrics are:
- Lightweight
- Fast to query
- Easy to aggregate
- Ideal for alerting

This is why:
- Most dashboards are metric-based
- Most alerts are metric-driven
- SLOs are built on metrics

If metrics are poorly designed, **everything on top becomes unreliable**.

---

## Metrics vs Logs vs Traces

Each signal serves a different purpose:

- **Metrics** → Overall system health
- **Logs** → Detailed events and errors
- **Traces** → Request-level execution flow

Metrics give the **big picture**.

---

## Metric Types in Datadog

Understanding metric types is critical.

---

### Gauge

Represents a value at a specific moment.

Examples:
- CPU usage
- Memory usage
- Queue depth

Characteristics:
- Can increase or decrease
- Represents current state

---

### Count

Represents how many times something happened.

Examples:
- Requests served
- Errors occurred

Characteristics:
- Monotonically increasing
- Aggregated over time

---

### Rate

Represents how fast something is happening.

Examples:
- Requests per second
- Errors per minute

Usually derived from counts.

---

### Distribution

Captures many values to calculate percentiles.

Examples:
- Request latency
- Database query duration

Enables:
- p50, p95, p99

---

## Host Metrics vs Custom Metrics

### Host Metrics
- Collected automatically
- Infrastructure-focused

Examples:
- CPU
- Memory
- Disk
- Network

---

### Custom Metrics
- Defined by applications or teams
- Business or application focused

Examples:
- Checkout success rate
- Orders per minute

Custom metrics require **careful design** to avoid cost issues.

---

## Metric Naming Best Practices

Good metric names:
- Are descriptive
- Follow a hierarchy
- Are consistent

Examples:
- `http.requests.total`
- `db.query.latency`

Bad names:
- `metric1`
- `test_value`

---

## Tags on Metrics

Tags make metrics usable.

Tags enable:
- Filtering
- Grouping
- Comparison

Example:
```
metric: http.requests.total
tags: env:prod, service:checkout, region:ap-south-1
```

---

## Aggregation (Critical Concept)

Metrics are aggregated over time.

Common aggregations:
- avg
- sum
- min
- max
- count

Choosing the wrong aggregation:
> Changes the meaning of the metric.

---

## Common Metric Mistakes

❌ High-cardinality tags  
❌ Alerting on noisy metrics  
❌ Poor naming conventions  
❌ No documentation for custom metrics  

---

## Key Takeaways

- Metrics are time-series data
- Metric type defines behavior
- Tags define usability
- Aggregation defines meaning
- Metrics power dashboards and alerts

---

➡️ **Next Module:** Advanced Metrics Concepts
