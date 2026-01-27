---
sidebar_position: 5
title: IAM Policy Conditions
---

# IAM Policy Conditions

IAM Policy Conditions allow you to make permissions **context-aware**.
Instead of only saying *what* is allowed,
👉 conditions define **when, how, and under what circumstances** actions are allowed.

This is where IAM becomes **enterprise-grade security**.

---

## Why IAM Conditions Matter

Without conditions:
- Permissions are too broad
- Security relies only on identity

With conditions, you can:
- Enforce MFA
- Restrict access by IP
- Limit access by time
- Control access based on AWS context

👉 Conditions help enforce **least privilege properly**.

---

## What Is a Condition? (Simple Explanation)

A condition:
- Is an optional part of an IAM policy
- Evaluated during permission checks
- Must evaluate to **true** for access to be allowed

In simple terms:
> **Condition = extra security rule on top of permissions**

---

## Where Conditions Are Used

Conditions can be applied in:
- IAM permission policies
- Resource-based policies
- Trust policies (roles)

They work across:
- Users
- Roles
- AWS services

---

## Condition Structure (Basic Example)

```json
{
  "Effect": "Allow",
  "Action": "ec2:StartInstances",
  "Resource": "*",
  "Condition": {
    "Bool": {
      "aws:MultiFactorAuthPresent": "true"
    }
  }
}
```

This means:
- EC2 instances can be started
- **Only if MFA is enabled**

---

## Common Condition Keys (Must Know)

### aws:MultiFactorAuthPresent
- Enforces MFA
- Common for admin actions

### aws:SourceIp
- Restricts access by IP range

### aws:CurrentTime
- Time-based access control

### aws:RequestedRegion
- Restrict actions to specific regions

---

## Enforcing MFA (Very Common)

Example use case:
- Allow sensitive actions only if MFA is enabled

Used for:
- Admin access
- Production changes

👉 MFA enforcement is **mandatory in real environments**.

---

## IP-Based Restrictions

You can restrict access:
- From corporate network
- From known IP ranges

Example:
- Allow AWS Console access only from office IP

⚠️ Be careful with dynamic IPs.

---

## Time-Based Access

Conditions allow:
- Office-hours access
- Temporary access windows

Example:
- Allow access only between 9 AM and 6 PM

Used for:
- Contractors
- Temporary roles

---

## Region Restrictions

Restrict actions to:
- Approved AWS regions only

Example:
- Block resource creation outside `us-east-1`

👉 Helps with compliance and cost control.

---

## Combining Multiple Conditions

Conditions can be combined:
- MFA + IP restriction
- Time + region restriction

All conditions must evaluate to **true**.

---

## Common Beginner Mistakes

- Forgetting conditions exist
- Locking yourself out with strict policies
- Misunderstanding condition operators
- Not testing policies

Always:
- Test with least privilege
- Use IAM Policy Simulator

---

## Interview Tip

If asked:
> “How do you enforce MFA using IAM?”

Strong answer:
> By using IAM policy conditions such as aws:MultiFactorAuthPresent to restrict sensitive actions unless MFA is enabled.

This shows **advanced IAM understanding**.

---

## Key Takeaways

- Conditions add context to permissions
- Enable MFA, IP, time, and region controls
- Critical for enterprise security
- Must be tested carefully
- Separate good IAM from great IAM

---

📌 **Next:** Resource-Based Policies
