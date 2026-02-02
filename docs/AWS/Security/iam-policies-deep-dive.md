---
sidebar_position: 3
title: IAM Policies Deep Dive
---

# IAM Policies – Deep Dive

IAM policies are the **heart of AWS security**.
They define **exactly what actions are allowed or denied** in your AWS account.

Most IAM confusion comes from **not understanding policy structure properly**.
This page fixes that.

---

## What Is an IAM Policy?

An IAM policy is a JSON document that defines:
- Allowed or denied actions
- On specific AWS resources
- Under specific conditions

In simple terms:
> **IAM policy = rulebook for permissions**

---

## Types of IAM Policies

### Identity-Based Policies
- Attached to users, groups, or roles
- Most commonly used

### Resource-Based Policies
- Attached directly to resources (S3, SQS, SNS, etc.)
- Define who can access the resource

👉 Both are evaluated together.

---

## IAM Policy Structure (Must Know)

A policy contains:

- Version
- Statement
- Effect
- Action
- Resource
- Condition (optional)

Understanding this structure removes 80% of IAM fear.

---

## Policy Version

Example:
```json
"Version": "2012-10-17"
```

This defines:
- Policy language version
- Always use the latest version

---

## Statement Block

A policy can have:
- One or multiple statements

Each statement is evaluated independently.

---

## Effect

Defines:
- Allow
- Deny

Example:
```json
"Effect": "Allow"
```

⚠️ Explicit **Deny always overrides Allow**.

---

## Action

Defines:
- What API actions are allowed or denied

Examples:
```json
"s3:GetObject"
"ec2:StartInstances"
```

You can:
- Allow specific actions
- Use wildcards (carefully)

---

## Resource

Defines:
- Which resources the actions apply to

Examples:
```json
"arn:aws:s3:::my-bucket/*"
"arn:aws:ec2:region:account:instance/*"
```

Best practice:
- Avoid using `"*"` unless required

---

## Condition (Very Important)

Conditions restrict when permissions apply.

Examples:
- IP address
- MFA authentication
- Time-based access
- Tags

Conditions enforce **strong security controls**.

---

## Example: Simple S3 Read Policy

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::my-bucket/*"
    }
  ]
}
```

This allows:
- Read-only access to objects in a bucket

---

## IAM Policy Evaluation Logic (Critical)

AWS evaluates policies in this order:

1. Explicit Deny
2. Explicit Allow
3. Default Deny

Rule:
> **If not explicitly allowed, it is denied**

---

## Managed vs Inline Policies

### Managed Policies
- Reusable
- Recommended
- Easier to manage

### Inline Policies
- Attached to a single identity
- Harder to manage

👉 Prefer managed policies.

---

## Least Privilege in Policies

Good policies:
- Allow only required actions
- Restrict resources
- Use conditions

Bad policies:
- `"Action": "*"`
- `"Resource": "*"`

---

## Common Policy Mistakes

- Overusing wildcards
- No conditions
- Ignoring explicit deny
- Attaching admin policies everywhere

These mistakes lead to:
- Security breaches

---

## Debugging IAM Policies

Use:
- IAM Policy Simulator
- CloudTrail logs
- Error messages

Never:
- Guess permissions blindly

---

## Interview Tip

If asked:
> “How do IAM policies work?”

Strong answer:
> IAM policies are JSON documents that explicitly allow or deny actions on AWS resources, evaluated using deny-first logic.

---

## Key Takeaways

- Policies define permissions in AWS
- Structure understanding is critical
- Deny always wins
- Conditions enhance security
- Least privilege is mandatory

---

📌 **Next:** IAM Roles and Trust Policies
