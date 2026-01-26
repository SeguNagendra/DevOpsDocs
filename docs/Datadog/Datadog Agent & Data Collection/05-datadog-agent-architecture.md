---
sidebar_position: 1
---

# Datadog Agent Architecture

> *“The Datadog Agent is the bridge between your systems and observability.”*

This module belongs to **PHASE 3: Datadog Agent & Data Collection**.  
Here, we focus on **how the Datadog Agent works internally**, not how to install it yet.

Understanding the agent architecture will make:
- Troubleshooting easier
- Scaling safer
- Cost control smarter

---

## What Is the Datadog Agent?

The **Datadog Agent** is a lightweight software component that runs **alongside your systems** and is responsible for:

- Collecting telemetry data
- Enriching data with metadata (tags)
- Sending data securely to Datadog

It acts as the **data collection layer** of the Datadog platform.

---

## Why the Agent Is So Important

Almost everything in Datadog starts with the agent:

- Infrastructure metrics
- Custom application metrics
- Logs
- Traces (APM)
- Process and network data

If the agent is:
- Misconfigured → data is missing
- Overloaded → performance suffers
- Poorly understood → costs increase

---

## High-Level Agent Design

The Datadog Agent is designed to be:

- Lightweight
- Modular
- Secure
- Extensible

It runs as:
- A system service (VMs, bare metal)
- A container (Docker)
- A DaemonSet (Kubernetes)

---

## Modular Architecture (Core Concept)

The agent is **not a single monolithic process**.

It consists of multiple components, each responsible for a specific function.

At a high level:

- Core Agent
- Metrics Collection
- Log Collection
- APM & Tracing
- Process & Network Monitoring

Each module can be:
- Enabled or disabled
- Configured independently

---

## Core Agent

The **Core Agent** is responsible for:

- Managing configuration
- Handling credentials and keys
- Scheduling checks
- Orchestrating other components

Think of it as:
> *The coordinator of the entire agent system.*

---

## Metrics Collection Component

This component:
- Runs built-in checks
- Collects host-level metrics
- Collects integration metrics

Examples:
- CPU, memory, disk
- Nginx metrics
- Database metrics

Metrics are:
- Aggregated locally
- Sent periodically to Datadog

---

## Log Collection Component

The log agent:
- Collects logs from files, containers, or streams
- Applies processing rules (basic)
- Sends logs securely

Important:
- Logs are optional
- Explicitly enabled
- Cost-sensitive

---

## APM & Tracing Component

The APM agent:
- Receives traces from applications
- Groups spans into traces
- Applies sampling rules

This component works closely with:
- Language-specific libraries
- Application instrumentation

---

## Process & Network Monitoring

Optional components include:
- Process Agent (running processes)
- Network Performance Monitoring (traffic flows)

Used to:
- Understand host behavior
- Debug resource contention
- Analyze service dependencies

---

## Security Model (High Level)

The agent:
- Uses outbound HTTPS only
- Never accepts inbound traffic
- Uses API keys for authentication

Best practices:
- Protect API keys
- Limit host permissions
- Regularly update agent versions

---

## Agent vs Agentless (Conceptual)

Agent-based:
- Rich data
- Low latency
- Full correlation

Agentless:
- Limited visibility
- Useful for specific cloud services

Datadog is **agent-first by design**.

---

## What We Are NOT Doing Yet

This module does NOT cover:
- Installation steps
- Kubernetes manifests
- Configuration files
- Troubleshooting commands

Those belong to the **next modules** in this phase.

---

## Why This Module Matters

Understanding the agent:
- Prevents blind spots
- Improves performance
- Reduces costs
- Makes scaling predictable

---

## Key Takeaways

- Agent is the data collection backbone
- Modular architecture enables flexibility
- Each component has a clear role
- Agent-first approach provides deep visibility

---

➡️ **Next Module:** Agent Installation & Lifecycle
