---
sidebar_position: 2
---

# Agent Installation & Lifecycle

> *“Installing the agent is easy. Operating it correctly over time is the real skill.”*

This module belongs to **PHASE 3: Datadog Agent & Data Collection**.  
Here we focus on **where the Datadog Agent runs, how it is installed conceptually, and how it is managed throughout its lifecycle**.

We intentionally avoid deep command-level steps here — those come later when context is clear.

---

## Where the Datadog Agent Runs

The Datadog Agent always runs **close to the workload** it observes.

Common environments:
- Virtual machines (cloud or on‑prem)
- Bare metal servers
- Docker containers
- Kubernetes clusters

Key idea:
> The agent must see the system from the inside to observe it properly.

---

## Installation Models (Conceptual)

Datadog supports multiple installation models depending on the platform.

### Host-Based Installation
Used for:
- EC2 / VM-based workloads
- Traditional servers

Agent runs as:
- A system service
- One agent per host

---

### Container-Based Installation
Used for:
- Docker-based environments

Agent runs as:
- A dedicated container
- Collects metrics and logs from other containers

---

### Kubernetes Installation
Used for:
- Kubernetes clusters

Agent runs as:
- A DaemonSet (node-level visibility)
- Optional Cluster Agent (cluster-level visibility)

Kubernetes installs are **agent-heavy by design** due to dynamic workloads.

---

## Environment-Specific Considerations

Different environments require different thinking.

Examples:
- Production → stability and controlled upgrades
- Staging → testing new agent versions
- Development → limited data collection

Best practice:
> Treat the agent like any other production dependency.

---

## Agent Configuration Basics (High Level)

Agent behavior is controlled by configuration files and environment variables.

Conceptually, you configure:
- What data is collected
- Which features are enabled
- How data is tagged
- How often data is sent

We will deep dive into configuration files later.

---

## Agent Lifecycle Stages

The Datadog Agent has a clear lifecycle:

1. Install
2. Configure
3. Run
4. Upgrade
5. Troubleshoot
6. Retire

Each stage requires:
- Planning
- Validation
- Ownership

---

## Upgrading the Datadog Agent

Upgrades are important because:
- New features are added
- Bugs are fixed
- Security issues are resolved

Best practices:
- Upgrade in lower environments first
- Roll out gradually
- Monitor agent health after upgrades

Avoid:
> Large version jumps without testing

---

## Agent Health & Stability

A healthy agent:
- Uses minimal CPU and memory
- Sends data consistently
- Logs no persistent errors

Unhealthy agents cause:
- Missing data
- Delayed alerts
- False confidence

---

## Common Installation Mistakes

❌ Installing agent without tagging strategy  
❌ Enabling all features blindly  
❌ Ignoring agent upgrades  
❌ No ownership for agent health  

---

## Why Lifecycle Management Matters

Poor lifecycle management leads to:
- Data gaps
- Increased costs
- Hard-to-debug issues

Good lifecycle management leads to:
- Reliable telemetry
- Predictable behavior
- Easier scaling

---

## Key Takeaways

- Agent placement matters
- Installation model depends on platform
- Agent must be treated as a production component
- Lifecycle management is critical

---

➡️ **Next Module:** Auto‑Discovery & Integrations
