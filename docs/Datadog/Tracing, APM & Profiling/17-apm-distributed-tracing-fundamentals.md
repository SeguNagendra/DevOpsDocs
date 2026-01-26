---
sidebar_position: 1
---

# APM & Distributed Tracing Fundamentals

> *“If metrics show the problem and logs explain it, traces show you exactly where it happens.”*

This module belongs to **PHASE 9: Tracing, APM & Profiling**.  
Here we build a **clear mental model** of Application Performance Monitoring (APM) and distributed tracing before touching any tooling details.

---

## What Is APM?

**Application Performance Monitoring (APM)** focuses on understanding:
- How requests flow through applications
- Where time is spent
- Where errors originate

APM answers questions like:
- Why is this API slow?
- Which service is failing?
- Which dependency is the bottleneck?

---

## Why APM Is Critical in Microservices

In monolithic apps:
- One request → one process

In microservices:
- One request → many services

Without APM:
- Latency is invisible
- Root cause is unclear
- Teams blame the wrong service

APM provides:
> End-to-end visibility across services.

---

## What Is a Trace?

A **trace** represents a **single request** as it moves through a system.

A trace shows:
- Total request duration
- All services involved
- Timing of each operation

Think of a trace as:
> *A timeline of a request’s life.*

---

## What Is a Span?

A **span** is a single unit of work within a trace.

Examples:
- HTTP request handling
- Database query
- External API call

A trace is made up of:
> Multiple spans linked together.

---

## Trace Context Propagation

For tracing to work:
- Context must travel with the request
- Each service must pass trace IDs downstream

This process is called:
> **Context propagation**

Without it:
- Traces break
- Visibility is lost

---

## Services in APM

In Datadog:
- Services represent logical application components
- Identified by the `service` tag

Examples:
- checkout-api
- payment-service
- auth-service

Services are the **top-level unit** in APM.

---

## Key APM Signals

APM focuses on three primary signals:

- Latency → How long requests take
- Errors → What fails
- Throughput → How much traffic flows

These signals form the basis of:
- Performance dashboards
- Alerts
- SLOs

---

## APM vs Metrics (Important Distinction)

- Metrics → Aggregated behavior
- APM → Individual request behavior

Metrics tell you:
> *Something is slow*

APM tells you:
> *Which request, where, and why*

---

## Common APM Use Cases

APM is used for:
- Debugging slow APIs
- Finding failing dependencies
- Understanding service interactions
- Performance optimization

---

## Common Misconceptions

❌ APM replaces logs  
❌ APM is only for developers  
❌ APM is too expensive to use  

✅ APM complements metrics and logs  
✅ APM is critical for SREs and DevOps  
✅ Sampling controls cost  

---

## Why This Module Matters

Without APM fundamentals:
- Traces feel confusing
- Service maps feel random
- Debugging is slower

With APM fundamentals:
- Traces feel intuitive
- Bottlenecks stand out
- Incidents resolve faster

---

## Key Takeaways

- APM provides request-level visibility
- Traces show request journeys
- Spans represent work units
- Context propagation is essential
- APM complements metrics and logs

---

➡️ **Next Module:** Advanced APM & Sampling
