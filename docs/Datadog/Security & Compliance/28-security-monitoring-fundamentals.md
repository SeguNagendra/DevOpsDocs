---
sidebar_position: 1
---

# Security Monitoring Fundamentals

> *“Security incidents are operational incidents with higher stakes.”*

This module belongs to **PHASE 13: Security & Compliance**.  
Here we introduce **how Datadog approaches security visibility**, and how security signals fit naturally into observability workflows.

---

## What Is Security Monitoring?

Security monitoring focuses on detecting:
- Unauthorized access
- Suspicious behavior
- Policy violations
- Runtime threats

Unlike traditional security tools:
- Signals are continuous
- Context comes from infrastructure and applications
- Response often overlaps with incident management

---

## Why Security Belongs with Observability

Security incidents often look like:
- Performance issues
- Configuration mistakes
- Unexpected behavior

Observability data helps answer:
- What happened?
- When did it start?
- What systems were affected?

Datadog treats security as:
> *Another form of system behavior to observe.*

---

## Security Signals in Datadog

Datadog security monitoring uses:
- Logs (audit, access, auth)
- Metrics (unusual patterns)
- Events (changes, violations)
- Runtime signals (process behavior)

Correlation is key:
> One signal alone rarely tells the full story.

---

## Cloud Security Posture Management (CSPM)

CSPM focuses on:
- Cloud configuration correctness
- Security best practices
- Compliance standards

Examples:
- Public storage exposure
- Weak IAM policies
- Missing encryption

CSPM helps prevent:
> Security incidents before they happen.

---

## Runtime Security (High Level)

Runtime security monitors:
- What is running
- What processes are executed
- Unexpected behavior at runtime

It helps detect:
- Compromised containers
- Suspicious commands
- Malware-like activity

---

## Security vs Compliance

- Security → Prevent and detect threats
- Compliance → Prove controls exist

They overlap but are not the same.

Datadog supports both by:
- Monitoring continuously
- Retaining evidence
- Providing audit visibility

---

## Integrating Security with Incident Response

Security incidents:
- Follow similar lifecycles as outages
- Require fast detection and context

Datadog helps by:
- Correlating security signals with infra and app data
- Using existing alerting and incident workflows

---

## Common Security Monitoring Mistakes

❌ Treating security as separate from ops  
❌ Relying only on periodic scans  
❌ Ignoring runtime behavior  
❌ No ownership of security alerts  

---

## Why This Module Matters

Without security monitoring:
- Breaches go unnoticed
- Investigations are slow
- Compliance evidence is missing

With security monitoring:
- Threats are detected early
- Context is immediately available
- Response is faster and calmer

---

## Key Takeaways

- Security is continuous, not periodic
- Observability data powers security insights
- CSPM prevents misconfigurations
- Runtime security detects active threats

---

➡️ **Next Module:** Compliance, Audit Logs & Governance
