---
sidebar_position: 1
---

# Events & Change Tracking

> *“Most incidents are caused by change. Events help you see the change.”*

This module belongs to **PHASE 6: Events, Changes & Context**.  
Here we focus on **understanding what changed in your system and when**, and how that context dramatically speeds up incident investigation.

---

## What Is an Event?

An **event** represents a **point-in-time change** in your system.

Unlike metrics (which are continuous), events are:
- Discrete
- Time-bound
- Context-rich

Examples of events:
- Deployments
- Configuration changes
- Scaling actions
- Restarts
- Failovers

---

## Why Events Matter So Much

When an alert fires, the first question is almost always:

> **“What changed?”**

Without events:
- Teams guess
- Rollbacks are delayed
- Root cause analysis takes longer

With events:
- Changes are visible instantly
- Correlation becomes obvious
- Mean Time To Resolution (MTTR) drops

---

## Events vs Metrics vs Logs

Understanding the difference helps avoid misuse.

- Metrics → Continuous behavior over time
- Logs → Detailed records of actions
- Events → Significant changes

Events provide **context**, not volume.

---

## Common Sources of Events

Events can come from many places:

- Application deployments
- Infrastructure scaling (auto-scaling)
- Configuration updates
- CI/CD pipelines
- Cloud provider changes

In Datadog, these sources are unified into a single event stream.

---

## Deployment Events

Deployment events are one of the **most valuable event types**.

They answer:
- When was new code released?
- Which version went live?
- Which service was affected?

Best practice:
> Always emit deployment events for production releases.

---

## Configuration Change Tracking

Configuration changes often cause subtle issues.

Examples:
- Feature flags toggled
- Environment variables updated
- Resource limits changed

Tracking config changes helps:
- Correlate issues with changes
- Avoid blind rollbacks

---

## Events on Dashboards

Events can be displayed directly on dashboards.

Benefits:
- See changes alongside metrics
- Quickly correlate spikes or drops
- Reduce investigation time

Example:
- Latency spike aligned with deployment event

---

## Events in Incident Investigation

During incidents, events help you:
- Narrow down the timeline
- Identify triggering changes
- Decide rollback vs fix

Without events:
> Incident response becomes guesswork.

---

## Noise vs Signal in Events

Not all events are useful.

Good events:
- Meaningful
- Actionable
- Limited in volume

Bad events:
- Too frequent
- Too generic
- No context

Best practice:
> Track important changes, not every action.

---

## Common Mistakes

❌ Not emitting deployment events  
❌ Too many low-value events  
❌ No ownership for event sources  
❌ Ignoring events during incidents  

---

## Why This Module Matters

Events connect:
- Metrics → behavior
- Logs → details
- Traces → execution

They complete the observability picture by answering:
> *What changed when the problem started?*

---

## Key Takeaways

- Events represent change
- Change causes most incidents
- Events provide critical context
- Dashboards + events = faster RCA

---

➡️ **Next Phase:** Dashboards & Visualization
