---
sidebar_position: 8
title: AWS Config
---

# AWS Config

Monitoring tells you **how systems behave**.
Auditing tells you **who did what**.
👉 **AWS Config tells you how your resources are configured over time.**

AWS Config is a **configuration tracking and compliance service**.
It answers one critical question:

> “What changed, when did it change, and is it compliant?”

---

## What Is AWS Config? (Simple Explanation)

AWS Config:
- Records configuration changes of AWS resources
- Maintains historical configuration snapshots
- Evaluates resources against compliance rules

In simple terms:
> **AWS Config = configuration history + compliance engine**

---

## Why AWS Config Exists

Without AWS Config:
- No visibility into configuration drift
- Hard to prove compliance
- Difficult root cause analysis

AWS Config exists to:
- Track configuration changes
- Detect drift from standards
- Enforce governance

👉 Essential for **regulated and enterprise environments**.

---

## What AWS Config Tracks

AWS Config records:
- Resource creation
- Configuration updates
- Resource deletion

Examples:
- Security Group rule changes
- S3 bucket public access changes
- IAM policy modifications
- EC2 instance attribute changes

---

## Configuration Items (CI)

Each recorded change creates a:
- **Configuration Item (CI)**

A CI contains:
- Resource state
- Relationships
- Metadata
- Timestamp

This allows:
- Point-in-time configuration review

---

## Configuration History

AWS Config allows you to:
- View historical configurations
- Compare changes over time
- Roll back understanding

Use cases:
- Incident investigation
- Compliance audits
- Change management

---

## AWS Config Rules

Config Rules:
- Evaluate resources against conditions
- Mark resources as COMPLIANT or NON_COMPLIANT

Types of rules:
- AWS-managed rules
- Custom rules (Lambda-backed)

Examples:
- S3 buckets must not be public
- EC2 instances must use approved instance types
- IAM users must have MFA

---

## Managed vs Custom Rules

### AWS-Managed Rules
- Pre-built by AWS
- Easy to enable
- Cover common compliance needs

### Custom Rules
- Written using Lambda
- Highly flexible
- Used for custom standards

---

## Continuous vs Periodic Evaluation

Rules can run:
- On configuration change (continuous)
- On a schedule (periodic)

Choose based on:
- Compliance strictness
- Cost considerations

---

## AWS Config and Compliance

AWS Config helps with:
- Security audits
- Regulatory compliance (PCI, HIPAA, ISO)
- Internal governance

It provides:
- Evidence
- History
- Automated checks

---

## AWS Config vs CloudTrail (Important)

| Feature | CloudTrail | AWS Config |
|------|------------|------------|
| Purpose | Who did what | What changed |
| Focus | API activity | Resource configuration |
| Use case | Auditing | Compliance & drift |
| Time | Event-based | State-based |

👉 Both are complementary.

---

## Common Beginner Mistakes

- Assuming Config is enabled by default
- Not enabling required resource types
- Ignoring costs
- Not acting on NON_COMPLIANT resources

These mistakes reduce value.

---

## Interview Tip

If asked:
> “How do you track configuration changes in AWS?”

Strong answer:
> By using AWS Config to record configuration changes and evaluate resources against compliance rules.

This shows **governance-level understanding**.

---

## Key Takeaways

- AWS Config tracks configuration changes
- Provides historical visibility
- Enforces compliance rules
- Detects drift
- Essential for governance

---

📌 **Next:** Monitoring & Logging Summary
