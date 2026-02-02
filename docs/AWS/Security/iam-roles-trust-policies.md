---
sidebar_position: 4
title: IAM Roles and Trust Policies
---

# IAM Roles and Trust Policies

IAM roles are the **preferred way to grant permissions in AWS**.
They enable **secure, temporary access** without long-term credentials.

Understanding roles and trust policies is **mandatory for real-world AWS security**.

---

## What Is an IAM Role?

An IAM role:
- Has permissions (via policies)
- Has no long-term credentials
- Is assumed temporarily

In simple terms:
> **Role = set of permissions that can be assumed**

---

## Why IAM Roles Exist

IAM roles solve problems like:
- Hardcoded credentials
- Credential rotation
- Secure service-to-service access

Roles enable:
- Temporary credentials
- Least privilege access
- Better security posture

---

## Common IAM Role Use Cases

- EC2 accessing S3
- Lambda accessing DynamoDB
- ECS tasks accessing AWS services
- Cross-account access

👉 Almost all AWS services rely on roles.

---

## Trust Policy (Very Important)

A trust policy:
- Defines **who can assume the role**
- Is different from permission policies

Think of it as:
> **Trust policy = who is allowed to wear this role**

---

## Trust Policy Structure

A trust policy is also a JSON document.

Key elements:
- Effect
- Principal
- Action
- Condition (optional)

---

## Example: EC2 Trust Policy

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "Service": "ec2.amazonaws.com"
      },
      "Action": "sts:AssumeRole"
    }
  ]
}
```

This allows:
- EC2 instances to assume the role

---

## sts:AssumeRole (Key Concept)

When a role is used:
- AWS Security Token Service (STS) issues temporary credentials
- Credentials expire automatically

Benefits:
- No credential leaks
- Automatic rotation

---

## Permission Policies vs Trust Policies

| Policy Type | Purpose |
|-----------|--------|
| Trust Policy | Who can assume the role |
| Permission Policy | What the role can do |

👉 Both are required for a role to work.

---

## Service Roles

Service roles are:
- Roles assumed by AWS services
- Created automatically or manually

Examples:
- EC2 instance role
- Lambda execution role

---

## Cross-Account Roles

Used when:
- One AWS account needs access to another

How it works:
- Trust policy allows external account
- Permissions control allowed actions

Common in:
- Multi-account architectures

---

## Role Chaining (Brief)

Role chaining:
- One role assumes another role
- Limited session duration

Used carefully:
- Adds complexity

---

## Security Best Practices

- Use roles instead of access keys
- Restrict trust policies
- Enable MFA for sensitive roles
- Monitor role usage with CloudTrail

---

## Common Beginner Mistakes

- Confusing trust and permission policies
- Overly broad principals
- Using users instead of roles
- Not limiting role duration

These mistakes weaken security.

---

## Interview Tip

If asked:
> “How does an EC2 instance access AWS services securely?”

Strong answer:
> By using an IAM role attached to the instance, which provides temporary credentials via STS.

---

## Key Takeaways

- Roles provide temporary access
- Trust policies define who can assume roles
- STS issues temporary credentials
- Roles are central to AWS security
- Preferred over long-term credentials

---

📌 **Next:** IAM Best Practices and Security Patterns
