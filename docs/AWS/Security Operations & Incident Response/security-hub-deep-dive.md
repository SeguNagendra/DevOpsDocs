---
sidebar_position: 4
title: AWS Security Hub Deep Dive
---

# AWS Security Hub – Deep Dive

AWS Security Hub acts as the **central command center** for cloud security.
It aggregates, prioritizes, and visualizes security findings from across AWS and third-party tools.

If GuardDuty is the **sensor**,
👉 Security Hub is the **single pane of glass**.

---

## What Is AWS Security Hub? (Clear Explanation)

AWS Security Hub:
- Collects security findings from multiple sources
- Normalizes findings into a common format
- Provides compliance and security posture visibility

In simple terms:
> **Security Hub = centralized security findings and compliance dashboard**

---

## Why Security Hub Is Important

Without Security Hub:
- Findings are scattered
- Teams miss critical alerts
- No unified security posture

Security Hub provides:
- Central visibility
- Prioritized findings
- Compliance insights

---

## Security Hub Data Sources

Security Hub aggregates findings from:

- Amazon GuardDuty
- Amazon Inspector
- AWS Config
- IAM Access Analyzer
- Third-party security tools

This removes the need to:
- Check each service separately

---

## AWS Security Standards

Security Hub evaluates accounts against:

- **AWS Foundational Security Best Practices**
- **CIS AWS Foundations Benchmark**
- **PCI DSS** (if applicable)

Standards provide:
- Continuous compliance checks
- Security posture scores

---

## Findings Format (ASFF)

Security Hub uses:
- AWS Security Finding Format (ASFF)

ASFF includes:
- Resource details
- Severity
- Remediation guidance
- Compliance status

Standard format enables:
- Automation
- Tool integration

---

## Security Scores and Insights

Security Hub provides:
- Security score (percentage)
- Failed vs passed controls
- Trend insights

Scores help:
- Track improvement over time
- Communicate risk to leadership

---

## Severity and Prioritization

Findings have severities:
- Low
- Medium
- High
- Critical

Best practice:
> **Prioritize high & critical findings first**

---

## Automation with Security Hub

Security Hub integrates with:
- EventBridge
- Lambda
- SOAR tools

Common automations:
- Auto-remediate failed controls
- Create tickets (Jira, ServiceNow)
- Notify SOC teams

---

## Security Hub and Organizations

Best practice:
- Enable Security Hub organization-wide
- Use delegated admin account
- Aggregate findings centrally

This scales security operations.

---

## Security Hub vs GuardDuty

| Aspect | Security Hub | GuardDuty |
|-----|--------------|-----------|
| Purpose | Aggregation & compliance | Threat detection |
| Alerts | Centralized | Individual |
| Compliance | Yes | No |
| Investigation | Limited | Detection only |

They work **together**, not separately.

---

## Cost Considerations

Security Hub pricing is based on:
- Number of security checks
- Ingested findings

Best practice:
- Enable required standards only
- Review findings regularly

---

## Common Beginner Mistakes

- Treating Security Hub as detection tool
- Ignoring compliance findings
- No ownership for findings
- No automation

These reduce its value.

---

## Interview Tip

If asked:
> “How do you centralize security findings in AWS?”

Strong answer:
> By using AWS Security Hub to aggregate and prioritize findings from GuardDuty, Inspector, and AWS Config.

---

## Key Takeaways

- Security Hub centralizes security findings
- Provides compliance visibility
- Normalizes data using ASFF
- Works best with automation
- Essential for scaled SecOps

---

📌 **Next:** Amazon Inspector Deep Dive
