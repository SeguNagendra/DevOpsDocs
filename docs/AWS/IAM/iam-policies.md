---
sidebar_position: 4
title: IAM Policies
---

# IAM Policies

IAM Policies define **what actions are allowed or denied** in AWS.
They are the **core language of permissions**.

If IAM roles are *who* can act,
👉 **IAM policies define what actions are allowed**.

Understanding policies separates **basic users from real AWS engineers**.

---

## What Is an IAM Policy? (Simple Explanation)

An IAM policy is:
- A JSON document
- That defines permissions
- Evaluated by AWS on every request

In simple terms:
> **IAM Policy = rulebook for AWS permissions**

---

## Why IAM Policies Exist

Without policies:
- No fine-grained access control
- Everyone would have full access

Policies exist to:
- Enforce least privilege
- Control access precisely
- Support compliance and auditing

---

## Types of IAM Policies

AWS supports multiple policy types:

1. AWS Managed Policies  
2. Customer Managed Policies  
3. Inline Policies  

---

## AWS Managed Policies

- Created and maintained by AWS
- Easy to use
- Broad permissions

Examples:
- AdministratorAccess
- ReadOnlyAccess

⚠️ Useful for learning, **not ideal for production**.

---

## Customer Managed Policies (Best Practice)

- Created and managed by you
- Reusable
- Version-controlled

👉 **Preferred for real environments**.

---

## Inline Policies

- Embedded directly into a user/role
- Not reusable
- Harder to manage

⚠️ Avoid unless absolutely required.

---

## IAM Policy Structure (Must Know)

Every policy contains:

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

---

## Policy Elements Explained

### Effect
- Allow or Deny

### Action
- AWS API actions (e.g., s3:GetObject)

### Resource
- ARN of the resource

### Condition (Optional)
- Extra constraints (IP, MFA, time)

---

## Explicit Deny (Very Important)

Rules:
- Explicit Deny **always wins**
- Even if Allow exists

Used for:
- Blocking sensitive actions
- Guardrails

---

## Least Privilege Principle

Best practice:
- Grant only required permissions
- Avoid wildcards (`*`) when possible

Example:
- Allow specific S3 bucket
- Not all S3 resources

---

## Policy Evaluation Logic (High Level)

When AWS evaluates a request:
1. Check explicit Deny
2. Check Allow
3. Default = Deny

👉 Everything is denied unless allowed.

---

## Common Beginner Mistakes

- Using `*` everywhere
- Attaching policies directly to users
- Not testing policies
- Mixing trust and permission policies

These mistakes cause:
- Security risks
- Unexpected access failures

---

## Interview Tip

If asked:
> “How does AWS decide if an action is allowed?”

Strong answer:
> AWS evaluates IAM policies, where explicit deny overrides allow, and everything is denied by default unless explicitly permitted.

That shows **deep IAM understanding**.

---

## Key Takeaways

- IAM policies define permissions
- JSON-based rule documents
- Explicit deny overrides allow
- Least privilege is critical
- Core of AWS security model

---

📌 **Next:** IAM Policy Conditions and Advanced Scenarios
