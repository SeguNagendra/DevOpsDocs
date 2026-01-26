---
sidebar_position: 3
---

# Cloud Provider Monitoring

> *“In the cloud, many of your most critical components are not running on your servers.”*

This module belongs to **PHASE 10: Infrastructure & Platform Monitoring**.  
Here we focus on **monitoring managed cloud services and cloud-level signals**, with a conceptual emphasis on AWS-style environments.

---

## Why Cloud Provider Monitoring Is Different

Cloud providers manage:
- Databases
- Load balancers
- Queues
- Storage services

You cannot:
- SSH into them
- Install agents inside them

Yet:
> These services are often the most critical parts of your system.

---

## Datadog Cloud Integrations (High Level)

Datadog integrates with cloud providers by:
- Pulling metrics via APIs
- Ingesting events
- Enriching data with tags

This is often called:
> *Agentless monitoring*

---

## Commonly Monitored Cloud Services

Examples include:
- Compute services
- Managed databases
- Load balancers
- Message queues
- Storage systems

These services provide:
- Performance metrics
- Availability indicators
- Error signals

---

## Cloud Metrics vs Host Metrics

- Host metrics → OS-level behavior
- Cloud metrics → Service-level behavior

Example:
- Host CPU → VM resource usage
- Database latency → Managed service performance

Both are needed for:
> Complete visibility.

---

## Multi-Account Cloud Monitoring

In larger organizations:
- Workloads span multiple accounts
- Teams own different environments

Datadog supports:
- Centralized visibility
- Account-level separation
- Unified dashboards

Best practice:
> Monitor all accounts from a single Datadog org.

---

## Cloud Events & Change Visibility

Cloud providers emit events for:
- Scaling actions
- Failures
- Configuration changes

Tracking these events helps:
- Correlate incidents
- Detect misconfigurations
- Understand outages

---

## Managed Service Blind Spots

Common blind spots:
- Database saturation
- Throttling
- Quota exhaustion

Cloud monitoring helps detect:
> Issues before applications fail.

---

## Tagging Cloud Resources

Cloud integrations automatically generate tags.

Examples:
- Account
- Region
- Service type

Good tagging enables:
- Cost attribution
- Ownership clarity
- Cross-service correlation

---

## Common Mistakes

❌ Monitoring only compute  
❌ Ignoring managed service metrics  
❌ Separate dashboards per account  
❌ No cloud-level alerts  

---

## Why This Module Matters

Without cloud provider monitoring:
- Root causes are missed
- Managed service failures look mysterious
- Outages last longer

With proper monitoring:
- Issues are visible early
- Cloud complexity is manageable
- Platform reliability improves

---

## Key Takeaways

- Cloud services require agentless monitoring
- Managed services are critical dependencies
- Multi-account visibility is essential
- Cloud events provide valuable context

---

➡️ **Next Phase:** User Experience Monitoring
