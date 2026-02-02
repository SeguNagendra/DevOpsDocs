---
sidebar_position: 3
title: Service Control Policies (SCP) – Deep Dive
---

# Service Control Policies (SCP) – Deep Dive

Service Control Policies (SCPs) are the **strongest governance control** in AWS.
They define the **maximum permissions** that accounts can ever have.

If IAM policies say *what is allowed*,
👉 SCPs say *what is NEVER allowed*.

---

## What Is a Service Control Policy?

An SCP:
- Is a policy applied at **Organization, OU, or Account level**
- Sets permission boundaries for AWS accounts
- Does NOT grant permissions by itself

In simple terms:
> **SCPs restrict what IAM can ever allow**

---

## How SCPs Work (Very Important)

Effective permissions =
- IAM policies
- Resource policies
- Permission boundaries
- **SCPs (hard limit)**

If SCP denies an action:
> **No IAM policy can override it**

---

## SCP vs IAM Policies

| Aspect | SCP | IAM Policy |
|----|----|-----------|
| Scope | Account / OU | User / Role |
| Grants permissions | ❌ No | ✅ Yes |
| Denies actions | ✅ Yes | ✅ Yes |
| Override possible | ❌ No | ✅ Sometimes |

SCPs act as **guardrails**, not access tools.

---

## Common SCP Use Cases

Typical governance use cases:

- Restrict AWS regions
- Prevent root user actions
- Enforce encryption
- Block risky services
- Protect critical resources

---

## Example: Deny Non-Approved Regions

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Deny",
      "Action": "*",
      "Resource": "*",
      "Condition": {
        "StringNotEquals": {
          "aws:RequestedRegion": [
            "ap-south-1",
            "us-east-1"
          ]
        }
      }
    }
  ]
}
```

This prevents:
- Accidental resource creation in unwanted regions

---

## Example: Deny Root User Actions

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Deny",
      "Action": "*",
      "Resource": "*",
      "Condition": {
        "StringLike": {
          "aws:PrincipalArn": "arn:aws:iam::*:root"
        }
      }
    }
  ]
}
```

Root should be:
> **Used only for account setup**

---

## Allow List vs Deny List SCPs

Two approaches:

### Deny List (Recommended)
- Allow everything by default
- Explicitly deny dangerous actions

### Allow List
- Deny everything by default
- Explicitly allow required services

Allow list SCPs are:
- Very restrictive
- Easy to break workloads

---

## SCP Attachment Strategy

Attach SCPs to:
- OUs (preferred)
- Accounts (specific cases)

Best practice:
- Apply common guardrails at OU level
- Avoid account-by-account management

---

## SCP Evaluation Order

AWS evaluates:
1. SCPs
2. IAM permission boundaries
3. IAM policies

Any explicit deny:
> **Wins immediately**

---

## Testing SCPs Safely

Best practices:
- Test in sandbox OU
- Use AWS Policy Simulator
- Roll out gradually

Never:
- Apply SCPs directly to production without testing

---

## Common Beginner Mistakes

- Locking out admin access
- Using allow-list SCPs too early
- No documentation
- No break-glass account

These mistakes cause:
- Account lockouts

---

## Break-Glass Strategy

Always have:
- Emergency admin role
- Documented recovery process

Governance without recovery:
> **Is dangerous**

---

## Interview Tip

If asked:
> “How do you enforce governance across AWS accounts?”

Strong answer:
> By using AWS Organizations with Service Control Policies to enforce preventive guardrails.

---

## Key Takeaways

- SCPs define maximum permissions
- They override IAM policies
- Best used as preventive guardrails
- Deny-list strategy is safer
- Always test before production rollout

---

📌 **Next:** AWS Config and Compliance Rules
