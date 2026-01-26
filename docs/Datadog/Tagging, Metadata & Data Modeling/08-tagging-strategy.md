---
sidebar_position: 1
---

# Tagging Strategy (CRITICAL)

> *“If Datadog feels confusing or expensive, tagging is almost always the reason.”*

This module belongs to **PHASE 4: Tagging, Metadata & Data Modeling**.  
Tagging is **one of the most important concepts in Datadog** — it affects **clarity, scalability, alert quality, and cost**.

Many Datadog problems are not tool problems.  
They are **tagging problems**.

---

## What Is a Tag?

A **tag** is a simple `key:value` label attached to data.

Examples:
- `env:prod`
- `service:checkout`
- `team:payments`
- `region:ap-south-1`

Tags are applied to:
- Metrics
- Logs
- Traces
- Events
- Hosts and containers

---

## Why Tagging Matters So Much

Tags allow Datadog to:
- Filter data
- Group data
- Correlate signals
- Reuse dashboards
- Target alerts correctly

Without good tagging:
- Dashboards don’t scale
- Alerts fire incorrectly
- Costs increase silently

---

## Unified Service Tagging (Core Concept)

Datadog promotes **Unified Service Tagging**, which standardizes key tags across all signals.

The three most important tags:
- `env` → environment (prod, staging, dev)
- `service` → logical service name
- `version` → application version

When these are consistent:
- Logs link to traces
- Traces link to metrics
- Dashboards work everywhere

---

## Global Tags vs Local Tags

### Global Tags
- Applied to all data from a host or agent
- Usually environment or region level

Examples:
- `env:prod`
- `region:ap-south-1`

---

### Local Tags
- Applied to specific services or integrations
- More granular

Examples:
- `service:payment-api`
- `db:postgres`

Best practice:
> Use global tags sparingly, local tags deliberately.

---

## Tag Inheritance (Important Behavior)

Tags are inherited through the system.

For example:
- Host tags → container tags
- Container tags → service tags
- Service tags → metrics and traces

This inheritance enables:
- Automatic correlation
- Reduced configuration effort

---

## Environment Strategy

Do **not** create separate dashboards per environment.

Instead:
- Use the same dashboards
- Filter using `env` tag

Example:
- Dashboard variable: `env`
- Values: dev, staging, prod

This approach:
- Reduces duplication
- Improves consistency

---

## Cardinality (The Hidden Danger)

**Cardinality** refers to how many unique values a tag has.

Low cardinality (good):
- `env:prod`
- `region:us-east-1`

High cardinality (dangerous):
- `user_id:123456`
- `request_id:abcd-efgh`

High cardinality leads to:
- Increased costs
- Performance issues
- Hard-to-use dashboards

Golden rule:
> Never tag metrics with unbounded values.

---

## Good vs Bad Tag Examples

✅ Good:
- `service:orders`
- `team:platform`
- `env:prod`

❌ Bad:
- `timestamp:169234234`
- `uuid:xyz-123`
- `email:user@example.com`

---

## Ownership & Team Tags

Tags also represent **ownership**.

Common ownership tags:
- `team`
- `owner`
- `squad`

Benefits:
- Clear alert routing
- Better accountability
- Faster incident response

---

## Common Tagging Mistakes

❌ Inconsistent tag names (`env` vs `environment`)  
❌ Missing `service` tag  
❌ High-cardinality tags on metrics  
❌ Different tags for logs vs traces  

---

## Why This Module Is Critical

Bad tagging:
- Breaks correlation
- Increases Datadog cost
- Creates alert noise

Good tagging:
- Makes Datadog powerful
- Reduces effort
- Scales with teams

---

## Key Takeaways

- Tags connect everything in Datadog
- Unified Service Tagging is mandatory
- Control cardinality carefully
- Consistency beats creativity

---

➡️ **Next Module:** Metrics Fundamentals
