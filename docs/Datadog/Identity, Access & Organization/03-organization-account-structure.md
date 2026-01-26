---
sidebar_position: 1
---

# Organization & Account Structure

> *“Before data, dashboards, or alerts — you must decide **who owns what**.”*

This module **starts Phase 2** of the roadmap.  
Phase 2 is about **governance, ownership, and structure**.

If Phase 1 explained *what Datadog is*,  
Phase 2 explains *how Datadog is organized inside a company*.

---

## What Is a Datadog Organization?

A **Datadog Organization (Org)** is the **top-level container** in Datadog.

An org contains:
- Users
- Teams
- Dashboards
- Monitors
- Data (metrics, logs, traces)
- Billing and usage

Think of an org as:
> *One company or one major business unit.*

---

## Single Organization vs Multiple Organizations

### Single Organization (Most Common)

Used when:
- One company
- Shared platform team
- Centralized monitoring

Benefits:
- Easy correlation
- Single source of truth
- Easier dashboards

Trade-offs:
- Needs good access control
- Strong tagging discipline required

---

### Multiple Organizations

Used when:
- Very large enterprises
- Strict isolation needed
- Different billing units
- Compliance requirements

Benefits:
- Hard isolation
- Separate billing
- Independent teams

Trade-offs:
- Harder cross-team visibility
- Duplicate dashboards and monitors

---

## How Companies Usually Choose

| Scenario | Recommended |
|------|-------------|
| Startup / mid-size | Single org |
| Large enterprise | Single org + RBAC |
| Regulated workloads | Multiple orgs |
| MSP / SaaS provider | Multiple orgs |

Best practice:
> Start with **one org**, split only if required.

---

## Teams in Datadog

Datadog supports **Teams** to represent ownership.

Teams:
- Group users logically
- Own services, dashboards, and monitors
- Improve accountability during incidents

Examples:
- Platform Team
- Payments Team
- SRE Team

Teams are **not security boundaries**, but **organizational boundaries**.

---

## Ownership & Responsibility Model

A healthy Datadog setup answers:
- Who owns this service?
- Who receives alerts?
- Who maintains dashboards?

Best practice:
- Every service → one owning team
- Every monitor → clear owner
- Every dashboard → maintained

This avoids:
- Alert confusion
- Broken dashboards
- On-call chaos

---

## Environment Separation Strategy

Common environments:
- Dev
- QA
- Staging
- Production

Best practice:
- Same org
- Separate via tags
- Same dashboards reused

Example:
- `env:dev`
- `env:prod`

Avoid:
- Separate org per environment (unless compliance requires)

---

## Common Mistakes

❌ One org per engineer  
❌ No clear ownership  
❌ Dashboards with no maintainers  
❌ Alerts without teams  

---

## Why This Module Matters

Bad org design leads to:
- Confusing dashboards
- Alert fatigue
- Ownership gaps
- Scaling problems

Good org design leads to:
- Clear responsibility
- Faster incident response
- Clean Datadog growth

---

## Key Takeaways

- Organization is the top-level boundary
- Single org is usually best
- Teams define ownership
- Structure before scale

---

➡️ **Next Module:** Access Management & Security (RBAC)
