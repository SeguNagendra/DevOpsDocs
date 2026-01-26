---
sidebar_position: 2
---

# Container & Kubernetes Monitoring

> *“In Kubernetes, nothing is static — monitoring must understand constant change.”*

This module belongs to **PHASE 10: Infrastructure & Platform Monitoring**.  
Here we focus on **how infrastructure monitoring changes in containerized and Kubernetes environments**, and what Datadog observes at each layer.

---

## Why Container Monitoring Is Different

Traditional infrastructure monitoring assumes:
- Long-lived hosts
- Static processes
- Predictable resource usage

Containers change this:
- Short-lived workloads
- Dynamic scheduling
- Shared resources

Monitoring must shift from:
> *hosts only → hosts + containers + orchestration*

---

## Containers as First-Class Citizens

In Datadog, containers are monitored as:
- Independent workloads
- Resource consumers
- Part of larger services

Container monitoring provides:
- CPU and memory per container
- Restart counts
- Resource limits vs usage

---

## Kubernetes Monitoring Layers

Kubernetes monitoring happens at **multiple layers**.

### Node Level
- CPU, memory, disk, network
- Similar to traditional hosts

### Pod Level
- Pod health and restarts
- Resource usage
- Scheduling issues

### Container Level
- Per-container resource usage
- OOM kills
- Throttling

---

## Kubernetes Control Plane Visibility

Beyond workloads, Kubernetes has a control plane.

Important components:
- API server
- Scheduler
- Controller manager
- etcd

Monitoring control plane health helps:
- Detect cluster-wide issues
- Prevent cascading failures

---

## Datadog Cluster Agent (Conceptual)

Datadog uses a **Cluster Agent** to:
- Collect cluster-level metrics
- Reduce load on node agents
- Enable advanced features

Think of it as:
> *The cluster-aware brain of Datadog.*

---

## Labels, Annotations & Tags

Kubernetes uses:
- Labels
- Annotations

Datadog converts these into:
- Tags

This enables:
- Filtering by namespace
- Grouping by app
- Correlating with services

---

## Common Kubernetes Metrics

Examples:
- Pod restart count
- CPU throttling
- Memory pressure
- Node readiness

These metrics help answer:
> *Is the cluster healthy or just the app failing?*

---

## Kubernetes Monitoring Use Cases

- Debugging CrashLoopBackOff
- Finding resource-hungry pods
- Understanding scaling behavior
- Detecting noisy neighbors

---

## Common Mistakes

❌ Monitoring only nodes  
❌ Ignoring pod-level metrics  
❌ No visibility into control plane  
❌ Missing resource limits  

---

## Why This Module Matters

Without container-aware monitoring:
- Issues are misdiagnosed
- Scaling problems are hidden
- On-call becomes painful

With proper monitoring:
- Problems are localized quickly
- Resource usage is understood
- Clusters scale confidently

---

## Key Takeaways

- Containers change monitoring fundamentals
- Kubernetes requires multi-layer visibility
- Cluster Agent enables advanced insights
- Tags connect Kubernetes to observability

---

➡️ **Next Module:** Cloud Provider Monitoring
