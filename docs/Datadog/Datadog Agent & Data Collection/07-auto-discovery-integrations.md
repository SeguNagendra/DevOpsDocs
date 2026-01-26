---
sidebar_position: 3
---

# Auto-Discovery & Integrations

> *“Modern infrastructure is dynamic. Observability must adapt automatically.”*

This module belongs to **PHASE 3: Datadog Agent & Data Collection**.  
Here we explain **how Datadog automatically discovers services and integrates with them**, without constant manual configuration.

This is a **core Datadog strength**, especially in containers and Kubernetes.

---

## Why Auto-Discovery Exists

In modern environments:
- Containers start and stop frequently
- Pods are recreated automatically
- IP addresses constantly change

Traditional monitoring fails because:
- Configurations become outdated
- Manual updates don’t scale
- Visibility gaps appear

Auto-discovery solves this by:
> Automatically detecting what is running and monitoring it.

---

## What Is Auto-Discovery in Datadog?

Auto-discovery is Datadog’s mechanism to:
- Detect services dynamically
- Apply the correct monitoring configuration
- Start collecting metrics and logs automatically

It removes the need to:
- Hardcode hostnames
- Manually edit config files for every service

---

## How Auto-Discovery Works (High Level)

At a conceptual level:

1. The agent scans the environment
2. It detects running services or containers
3. Matching integration templates are applied
4. Metrics and logs start flowing

This process repeats continuously.

---

## Auto-Discovery in Different Environments

### Virtual Machines
- Services detected via processes or ports
- Static but still automated

### Docker
- Containers detected automatically
- Metadata used for identification

### Kubernetes
- Pods and services detected dynamically
- Labels and annotations drive behavior

Auto-discovery is **most powerful in Kubernetes**.

---

## What Are Integrations?

An **integration** is a predefined way for Datadog to collect data from a system.

Integrations:
- Know what metrics to collect
- Follow best practices
- Reduce setup effort

Examples:
- Web servers
- Databases
- Message queues
- Cloud services

---

## Built-in Integrations

Datadog provides **hundreds of built-in integrations**.

They typically include:
- Standard metrics
- Default dashboards
- Suggested monitors

Benefits:
- Quick setup
- Consistent metrics
- Faster onboarding

---

## Custom Integrations (Conceptual)

When built-in integrations are not enough:
- Custom checks can be created
- Application-specific metrics collected

Use cases:
- Internal services
- Legacy systems
- Business-specific metrics

Custom integrations require:
- Strong metric design
- Careful cost consideration

---

## Logs & Auto-Discovery

Auto-discovery is not limited to metrics.

It also helps:
- Identify log sources
- Attach metadata automatically
- Route logs correctly

This ensures:
> Logs are searchable and correlated from day one.

---

## Common Mistakes

❌ Hardcoding service configurations  
❌ Disabling auto-discovery unnecessarily  
❌ Mixing static and dynamic configs  
❌ Ignoring metadata and labels  

---

## Why This Module Matters

Without auto-discovery:
- Monitoring does not scale
- Kubernetes visibility breaks
- Manual effort increases

With auto-discovery:
- Monitoring adapts automatically
- Visibility stays consistent
- Operations become easier

---

## Key Takeaways

- Auto-discovery adapts to dynamic systems
- Integrations simplify data collection
- Kubernetes benefits the most
- Less manual work, better visibility

---

➡️ **Next Phase:** Tagging, Metadata & Data Modeling
