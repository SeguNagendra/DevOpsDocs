---
sidebar_position: 7
title: AWS CloudTrail
---

# AWS CloudTrail

Monitoring tells you **how systems behave**.
👉 **Auditing tells you who did what.**

AWS CloudTrail is the **audit logging service** for AWS.
It records every API call made in your account.

If there is a security incident, CloudTrail is **the first place investigators look**.

---

## What Is AWS CloudTrail? (Simple Explanation)

AWS CloudTrail:
- Records AWS API calls
- Tracks who made the request
- Tracks when, where, and how the request was made

In simple terms:
> **CloudTrail = audit trail for AWS actions**

---

## Why CloudTrail Exists

Without CloudTrail:
- No accountability
- No forensic investigation
- No compliance evidence

CloudTrail exists to:
- Track user and service activity
- Support security audits
- Investigate incidents

👉 CloudTrail is **mandatory for production accounts**.

---

## What Does CloudTrail Log?

CloudTrail records:

- IAM actions
- Console logins
- AWS SDK / CLI calls
- Service-to-service API calls

Examples:
- `CreateInstance`
- `DeleteBucket`
- `AttachRolePolicy`
- `AssumeRole`

---

## CloudTrail Events (Types)

### Management Events
- Control-plane operations
- Enabled by default

Examples:
- Creating resources
- Updating IAM policies

---

### Data Events
- Object-level operations
- Disabled by default

Examples:
- S3 object access
- Lambda function invocation

⚠️ Data events can increase cost.

---

### Insight Events
- Detect unusual API activity
- Identify anomalies

Examples:
- Sudden spike in API calls
- Unusual access patterns

---

## Trails

A trail:
- Defines where CloudTrail logs are delivered
- Usually to S3 (and optionally CloudWatch Logs)

Best practice:
- One multi-region trail
- Centralized S3 bucket

---

## Multi-Region Trails (Best Practice)

Multi-region trail:
- Logs events from all regions
- Prevents blind spots

👉 Always enable **multi-region CloudTrail**.

---

## CloudTrail and CloudWatch Logs

CloudTrail can:
- Send events to CloudWatch Logs
- Enable near real-time alerts

Common use case:
- Alert on root account usage
- Alert on policy changes

---

## Security and Integrity

CloudTrail supports:
- Log file validation
- Encryption at rest
- Restricted access

Always:
- Encrypt logs
- Restrict S3 bucket access
- Enable log integrity validation

---

## Common Beginner Mistakes

- Not enabling CloudTrail
- Single-region trails only
- Ignoring data events when required
- Not monitoring CloudTrail logs

These mistakes cause:
- Security blind spots
- Compliance failures

---

## Interview Tip

If asked:
> “How do you audit AWS API activity?”

Strong answer:
> By using AWS CloudTrail to record and audit all API calls across the account.

This shows **security and compliance awareness**.

---

## Key Takeaways

- CloudTrail records AWS API activity
- Essential for auditing and security
- Management events are default
- Data events are optional but powerful
- Mandatory for production environments

---

📌 **Next:** AWS Config
