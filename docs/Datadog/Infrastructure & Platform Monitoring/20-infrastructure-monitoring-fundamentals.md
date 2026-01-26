---
sidebar_position: 1
---

# Infrastructure Monitoring Fundamentals

> *“Applications don’t fail in isolation — they fail because the infrastructure beneath them does.”*

This module belongs to **PHASE 10: Infrastructure & Platform Monitoring**.  
Here we focus on **monitoring the systems that run your applications** — hosts, processes, and underlying resources.

This phase shifts attention from *application behavior* to *platform health*.

---

## What Is Infrastructure Monitoring?

Infrastructure monitoring is about observing:
- Servers and virtual machines
- Operating system resources
- Processes running on hosts
- Network and disk behavior

It answers questions like:
- Is the host healthy?
- Are resources saturated?
- Is something leaking or stuck?

---

## Why Infrastructure Monitoring Still Matters

Even in cloud-native systems:
- CPUs can saturate
- Memory can leak
- Disks can fill up
- Networks can bottleneck

Ignoring infrastructure leads to:
> Treating symptoms instead of root causes.

---

## Hosts as the Core Unit

In Datadog, a **host** represents:
- A VM
- A bare-metal server
- A node in a Kubernetes cluster

Hosts are the foundation for:
- Host metrics
- Process visibility
- Network monitoring

---

## Core Host Metrics

Common host-level metrics include:

- CPU usage
- Memory utilization
- Disk I/O
- Disk space
- Network throughput

These metrics:
- Are collected automatically
- Provide early warning signals
- Power many alerts

---

## Process Monitoring (High Level)

Process monitoring shows:
- What processes are running
- How much CPU and memory they use
- How long they have been running

Use cases:
- Detect runaway processes
- Validate services are running
- Troubleshoot performance issues

---

## Host Maps

Host maps provide:
- Visual representation of infrastructure
- Grouping by tags
- Quick identification of outliers

They help answer:
> *Which host is behaving differently right now?*

---

## Infrastructure vs Application Monitoring

- Infrastructure monitoring → resource health
- Application monitoring → request behavior

Both are required.

Infrastructure issues often:
- Surface as application latency
- Appear as errors higher up the stack

---

## Tagging in Infrastructure Monitoring

Tags allow:
- Grouping hosts by environment
- Filtering by region or team
- Correlating infra with apps

Examples:
- `env:prod`
- `role:web`
- `region:ap-south-1`

---

## Common Infrastructure Monitoring Mistakes

❌ Relying only on cloud provider metrics  
❌ Ignoring disk and network metrics  
❌ Alerting only at host-level  
❌ No ownership of infrastructure alerts  

---

## Why This Module Matters

Strong infrastructure monitoring:
- Prevents cascading failures
- Improves incident response
- Builds confidence in the platform

Weak infrastructure monitoring:
- Hides root causes
- Increases downtime
- Slows debugging

---

## Key Takeaways

- Infrastructure health affects everything
- Hosts are foundational units
- Core metrics provide early signals
- Infrastructure and application monitoring complement each other

---

➡️ **Next Module:** Container & Kubernetes Monitoring
