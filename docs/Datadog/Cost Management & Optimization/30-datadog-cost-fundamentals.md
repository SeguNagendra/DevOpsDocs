---
sidebar_position: 1
---

# Datadog Cost Fundamentals

> *“Observability is powerful — but only when you understand what you are paying for.”*

This module belongs to **PHASE 14: Cost Management & Optimization**.  
Here we build a **clear mental model of Datadog pricing drivers**, so cost becomes **predictable and controllable**, not a surprise.

---

## Why Cost Management Matters in Datadog

Datadog cost issues usually happen because:
- Visibility grows faster than governance
- Data is ingested without strategy
- High-cardinality data goes unnoticed

Cost problems are rarely:
> A Datadog problem — they are a design problem.

---

## How Datadog Pricing Works (High Level)

Datadog pricing is based on:
- What data you send
- How much data you send
- How long you keep it

Different products have different cost units.

---

## Core Cost Drivers

### Infrastructure Monitoring
- Priced per host
- Includes core host metrics

Cost grows with:
- Number of hosts
- Agent footprint

---

### Metrics (Custom Metrics)
- Priced per custom metric
- Cardinality matters

Main drivers:
- Number of unique metric + tag combinations
- High-cardinality tags

---

### Logs
- Priced by log ingestion volume
- Indexed logs cost more
- Archived logs cost less

Key factor:
> Indexing decisions drive log cost.

---

### APM & Tracing
- Priced by analyzed traces
- Sampling controls cost

More traffic ≠ more cost if sampling is controlled.

---

### RUM & Synthetics
- Priced by sessions, events, and tests
- Frontend traffic directly affects cost

---

## Cardinality: The Silent Cost Killer

Cardinality increases when:
- Tag values are unbounded
- IDs are used as tags

Cardinality affects:
- Metrics
- Logs
- Traces

Golden rule:
> Control tags, control cost.

---

## Retention & Cost

Retention determines:
- How long data is stored
- How much historical analysis is possible

Shorter retention:
- Lower cost
- Less history

Longer retention:
- Higher cost
- More compliance value

---

## Cost Visibility in Datadog

Datadog provides:
- Usage dashboards
- Cost breakdowns
- Product-level consumption views

Best practice:
> Monitor Datadog with Datadog.

---

## Ownership & Cost Accountability

Cost should have owners.

Best practices:
- Tag data with `team` or `service`
- Review usage regularly
- Set expectations early

---

## Common Cost Mistakes

❌ No tagging strategy  
❌ Indexing all logs  
❌ No trace sampling  
❌ Ignoring usage dashboards  

---

## Why This Module Matters

Without cost awareness:
- Bills grow unpredictably
- Trust in observability drops

With cost awareness:
- Teams scale safely
- Visibility remains sustainable
- Datadog stays valuable

---

## Key Takeaways

- Datadog cost is data-driven
- Cardinality is the biggest risk
- Retention and indexing control spend
- Visibility enables optimization

---

➡️ **Next Module:** Cost Optimization Strategies
