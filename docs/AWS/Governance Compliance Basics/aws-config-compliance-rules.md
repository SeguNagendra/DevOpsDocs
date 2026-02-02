---
sidebar_position: 4
title: AWS Config and Compliance Rules
---

# AWS Config and Compliance Rules

Preventive controls stop bad actions.
**Detective controls tell you when something drifted or violated policy**.

AWS Config is the **core detective governance service** in AWS.

---

## What Is AWS Config?

AWS Config:
- Continuously records resource configurations
- Tracks configuration changes over time
- Evaluates resources against compliance rules

In simple terms:
> **AWS Config = configuration history + compliance checking**

---

## Why AWS Config Is Important

Without AWS Config:
- No configuration history
- No drift detection
- Weak audit evidence

With AWS Config:
- Full change visibility
- Continuous compliance
- Audit readiness

---

## What AWS Config Records

AWS Config tracks:
- Resource configuration details
- Relationship between resources
- Change timelines

Examples:
- Security group rule changes
- IAM policy updates
- S3 bucket configuration changes

---

## AWS Config Rules

Config Rules:
- Evaluate resource compliance
- Run continuously or on change

Rule types:
- AWS-managed rules
- Custom rules (Lambda-backed)

---

## Common AWS-Managed Config Rules

Examples:
- S3 bucket public access disabled
- EBS volumes encrypted
- IAM password policy compliant
- CloudTrail enabled

These provide:
- Quick compliance coverage

---

## Custom Config Rules

Custom rules allow:
- Organization-specific compliance logic

Implemented using:
- AWS Lambda

Use cases:
- Enforce tagging standards
- Validate custom security controls

---

## Compliance States

Each resource is:
- Compliant
- Non-compliant
- Not evaluated

This provides:
- Clear compliance visibility

---

## AWS Config and Organizations

Best practice:
- Enable Config across all accounts
- Use centralized aggregator account

This enables:
- Org-wide compliance view

---

## Remediation with AWS Config

Config integrates with:
- SSM Automation
- Lambda

Enable:
- Auto-remediation for simple issues

Example:
- Automatically enable encryption

---

## AWS Config vs CloudTrail

| Aspect | AWS Config | CloudTrail |
|----|-----------|-----------|
| Purpose | Compliance & drift | Audit logging |
| Tracks state | Yes | No |
| Detects changes | Yes | Yes |
| Evaluates rules | Yes | No |

They complement each other.

---

## Cost Considerations

AWS Config pricing is based on:
- Number of recorded resources
- Rule evaluations

Best practice:
- Enable selectively
- Focus on critical resources

---

## Common Beginner Mistakes

- Enabling Config but no rules
- No remediation setup
- Not aggregating across accounts
- Ignoring non-compliance

These reduce governance value.

---

## Interview Tip

If asked:
> “How do you detect configuration drift in AWS?”

Strong answer:
> By using AWS Config to track resource changes and evaluate compliance rules.

---

## Key Takeaways

- AWS Config is a detective control
- Tracks configuration history
- Evaluates compliance continuously
- Supports automation and remediation
- Essential for audits

---

📌 **Next:** Auditing with AWS CloudTrail
