---
sidebar_position: 1
---

# Agents & Scaling – Overview

This section explains **how Jenkins executes work at scale** using agents.
Understanding agents is critical for performance, cost control, and stability.

---

## Why Agents Matter

Without proper agent strategy:
- Builds queue endlessly
- Controllers get overloaded
- Costs increase
- Pipelines become flaky

Agents allow Jenkins to **scale horizontally**.

---

## Controller vs Agent (High-Level)

- **Controller**: Orchestrates jobs, schedules builds, manages state
- **Agents**: Execute pipeline steps (builds, tests, deployments)

> Controllers should not run heavy workloads.

---

## What Is a Jenkins Agent?

An agent is a machine (VM, container, pod, or bare metal) that:
- Connects to the controller
- Executes pipeline steps
- Provides tools and runtime environments

---

## Agent Types

Common agent types:
- Static agents (VMs / bare metal)
- Docker-based agents
- Kubernetes pod agents
- Cloud-based ephemeral agents

Each has different trade-offs.

---

## Executors

- Executors define **how many builds an agent can run concurrently**
- More executors ≠ better performance
- Executors compete for CPU, memory, disk

Proper sizing is critical.

---

## Label-Based Scheduling

Agents are selected using **labels**:
- OS-specific
- Tool-specific
- Capability-specific

Labels control where workloads run.

---

## Scaling Strategies

- Horizontal scaling (more agents)
- Ephemeral agents (on-demand)
- Workload isolation
- Auto-scaling via cloud/Kubernetes

---

## Common Scaling Problems

- Too many executors on one agent
- Running builds on controller
- No isolation between workloads
- Static agents for bursty workloads

---

## Security Considerations

- Agents execute arbitrary code
- Limit agent permissions
- Use ephemeral agents for untrusted code
- Separate prod and non-prod agents

---

## Interview Focus Areas

- Controller vs agent responsibilities
- Executors vs agents
- Horizontal vs vertical scaling

