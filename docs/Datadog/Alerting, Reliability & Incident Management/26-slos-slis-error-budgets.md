---
sidebar_position: 2
---

# SLOs, SLIs & Error Budgets

> *“Alerts tell you something is wrong. SLOs tell you if users are actually unhappy.”*

This module belongs to **PHASE 12: Alerting, Reliability & Incident Management**.  
Here we focus on **measuring reliability from the user’s point of view** and using those measurements to guide alerting and engineering decisions.

---

## What Is an SLI?

A **Service Level Indicator (SLI)** is a **measurable signal** that reflects user experience.

Examples:
- Request success rate
- Request latency
- Availability

SLIs answer:
> *How well is the service behaving right now?*

---

## What Is an SLO?

A **Service Level Objective (SLO)** is a **target value** for an SLI over a time window.

Example:
- 99.9% successful requests over 30 days

SLOs:
- Are goals, not guarantees
- Represent acceptable reliability

---

## SLOs vs SLAs

- SLA → Contractual promise (external)
- SLO → Internal engineering target

Best practice:
> Set SLOs stricter than SLAs.

---

## Error Budgets (Core Concept)

An **error budget** is the allowed amount of failure.

Example:
- 99.9% SLO → 0.1% error budget

Error budgets help teams decide:
- When to ship features
- When to focus on stability

Simple rule:
> No error budget → slow innovation  
> Too much error budget → unhappy users

---

## Why Error Budgets Matter

Error budgets:
- Balance speed and reliability
- Prevent over-alerting
- Enable data-driven decisions

They shift conversations from:
> “Is the system broken?”  
to  
> “Are we within our reliability target?”

---

## Burn Rate Alerts

Burn rate measures:
- How fast the error budget is being consumed

High burn rate:
- Means user experience is degrading quickly
- Requires immediate attention

Burn rate alerts:
> Catch incidents earlier than threshold alerts.

---

## SLO-Based Alerting

SLO alerts focus on:
- User impact
- Long-term reliability

Benefits:
- Fewer alerts
- Higher signal-to-noise ratio
- Better on-call experience

---

## Choosing Good SLIs

Good SLIs:
- Reflect user experience
- Are easy to measure
- Are stable over time

Avoid SLIs that:
- Are internal-only
- Don’t affect users
- Are hard to interpret

---

## Common Mistakes

❌ Too many SLOs  
❌ Unrealistic targets  
❌ Alerting on SLOs incorrectly  
❌ Ignoring error budget burn  

---

## Why This Module Matters

Without SLOs:
- Alerting is noisy
- Reliability is subjective
- Priorities are unclear

With SLOs:
- Reliability is measurable
- Decisions are data-driven
- Teams align on user impact

---

## Key Takeaways

- SLIs measure behavior
- SLOs define targets
- Error budgets enable balance
- Burn rate alerts detect risk early

---

➡️ **Next Module:** Incident Management & Postmortems
