---
sidebar_position: 2
---

# Datadog Platform Overview

> *“Before installing agents or creating alerts, you must understand **what Datadog is as a platform**.”*
 
It explains **how Datadog works at a platform level**, not *how to configure it yet*.

Think of this as learning the **map of the city** before driving through it.

---

## What Datadog Is (And What It Is Not)

Datadog is a **SaaS observability platform** that unifies:

- Metrics  
- Logs  
- Traces  
- Events  

into **one correlated system**.

Datadog is **not**:
- Just a dashboard tool  
- Just a logging platform  
- A replacement for good engineering practices  

Datadog **amplifies visibility**, it does not replace design.

---

## Why Datadog Exists

Modern systems are:
- Distributed
- Highly dynamic
- Cloud-native
- Microservice-based

Traditional monitoring tools fail because:
- They assume static infrastructure
- They treat signals in isolation
- They don’t scale with change

Datadog exists to:
> **Provide context, correlation, and clarity at scale**.

---

## Datadog as a SaaS Platform

Datadog runs as a **fully managed SaaS service**.

This means:
- You do not manage Datadog servers
- Scaling is handled automatically
- Storage, availability, and upgrades are managed

Your responsibility is limited to:
- Sending the right data
- Tagging it correctly
- Using it effectively

---

## High-Level Datadog Architecture

At a platform level, Datadog consists of:

1. **Your Systems**  
   - Applications  
   - Infrastructure  
   - Cloud services  

2. **Telemetry Ingestion Layer**  
   - Accepts metrics, logs, traces, events  

3. **Processing & Storage Layer**  
   - Aggregation  
   - Indexing  
   - Correlation  

4. **Analysis & Visualization Layer**  
   - Dashboards  
   - Monitors  
   - Exploration tools  

You will configure *each layer* in later phases.

---

## Control Plane vs Data Plane

This distinction is critical.

### Control Plane
The control plane is where you:
- Create dashboards
- Define monitors
- Configure SLOs
- Manage integrations

It defines **how Datadog behaves**.

---

### Data Plane
The data plane is where:
- Metrics
- Logs
- Traces
- Events

**flow through Datadog**.

It carries the **signals from your systems**.

---

## Unified Observability Model

Datadog does not treat telemetry in silos.

Instead:
- Metrics reference services
- Logs link to traces
- Traces link to infrastructure
- Events annotate everything

This correlation is what enables:
- Faster root cause analysis
- Reduced alert noise
- Better incident response

---

## Tag-Based Data Model (Conceptual Only)

Datadog uses **tags** to connect data.

At this stage, remember only this:
- Tags are simple key:value labels
- Tags apply to all data types
- Tags enable correlation

Example (do not implement yet):
- `env:prod`
- `service:checkout`
- `region:ap-south-1`

Tagging strategy is covered **later in depth**.

---

## Datadog User Interface (Orientation Only)

The Datadog UI is **use-case driven**, not tool-driven.

High-level areas:
- Observe → dashboards, explorers
- Alert → monitors, incidents
- Analyze → logs, traces, metrics
- Manage → configuration & settings

Goal of the UI:
> **Move from alert to understanding quickly**.

---

## What We Are NOT Doing Yet (Intentionally)

This module **does NOT cover**:
- Agent installation
- Integrations setup
- Logs pipelines
- APM instrumentation
- User & access management

Those belong to **later phases**.

---

## Why This Module Matters

Without this understanding:
- Datadog feels complex
- Features feel disconnected
- Costs feel unpredictable

With this understanding:
- Everything fits logically
- You know where each feature belongs
- Scaling Datadog becomes manageable

---

## Key Takeaways

- Datadog is a unified observability platform
- It is SaaS and fully managed
- Control plane defines behavior
- Data plane carries signals
- Correlation is Datadog’s superpower

---

➡️ **Next Module:** Organization & Account Structure
