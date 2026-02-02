---
sidebar_position: 5
title: Auditing and Logging with AWS CloudTrail
---

# Auditing and Logging with AWS CloudTrail

If it is not logged,
**it never happened** — at least from an auditor’s perspective.

AWS CloudTrail is the **primary auditing service** in AWS.
It provides a complete history of **who did what, when, and from where**.

---

## What Is AWS CloudTrail?

AWS CloudTrail:
- Records AWS API calls and events
- Tracks actions taken by users, roles, and services
- Stores logs for auditing and investigation

In simple terms:
> **CloudTrail = audit log for AWS accounts**

---

## Why CloudTrail Is Mandatory

Without CloudTrail:
- No audit trail
- No accountability
- No forensic evidence

With CloudTrail:
- Full visibility into API activity
- Compliance readiness
- Incident investigation support

---

## What CloudTrail Records

CloudTrail records:
- Management events (default)
- Data events (optional but important)
- Insights events (anomaly detection)

Examples:
- IAM role creation
- EC2 instance launch
- S3 object access

---

## Management Events

Management events track:
- Control plane operations
- Account-level changes

Examples:
- CreateUser
- AttachRolePolicy
- ModifySecurityGroup

Enabled by default.

---

## Data Events

Data events track:
- Object-level activity
- High-volume operations

Examples:
- S3 object read/write
- Lambda function invocation

Best practice:
- Enable selectively for critical resources

---

## CloudTrail Trails

A trail:
- Delivers events to S3
- Can cover one or all regions

Best practice:
- Create an **organization trail**
- Enable for all regions

---

## Organization Trails

Organization trails:
- Capture activity across all accounts
- Centralize logs in log archive account

This is essential for:
- Enterprise auditing
- Compliance

---

## Log Integrity and Security

Protect CloudTrail logs by:
- Storing in dedicated log archive account
- Enabling S3 versioning
- Enabling MFA delete (if possible)
- Restricting access tightly

Logs must be:
> **Tamper-resistant**

---

## CloudTrail and AWS Config

Together they provide:
- Who changed what (CloudTrail)
- What changed and compliance state (Config)

Auditors often require:
- Both

---

## CloudTrail Insights

CloudTrail Insights:
- Detects unusual API behavior
- Flags anomalies

Examples:
- Sudden spike in API calls
- Unusual IAM activity

Used for:
- Early threat detection

---

## Retention and Compliance

Best practices:
- Retain logs per compliance needs
- Use lifecycle policies
- Archive to Glacier if needed

Never:
- Delete audit logs prematurely

---

## Common Beginner Mistakes

- Single-region trail only
- No organization trail
- Logs stored in same account
- No access controls

These break audit readiness.

---

## Interview Tip

If asked:
> “How do you audit AWS activity?”

Strong answer:
> By enabling AWS CloudTrail organization trails to record all API activity centrally.

---

## Key Takeaways

- CloudTrail is the audit backbone
- Organization trails are best practice
- Data events provide deep visibility
- Log integrity is critical
- Essential for compliance and forensics

---

📌 **Next:** Compliance Programs and Audit Readiness
