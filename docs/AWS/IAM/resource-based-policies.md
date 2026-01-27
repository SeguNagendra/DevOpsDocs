---
sidebar_position: 6
title: Resource-Based Policies
---

# Resource-Based Policies

Resource-based policies are IAM policies that are **attached directly to AWS resources**.
Instead of saying *who* can act,
👉 they say **who can access this resource**.

They are essential for:
- Cross-account access
- Service-to-service permissions
- Fine-grained resource security

---

## What Is a Resource-Based Policy? (Simple Explanation)

A resource-based policy:
- Is attached to a resource (not a user or role)
- Defines **who** can access the resource
- Defines **what actions** are allowed
- Can allow **cross-account access**

In simple terms:
> **Resource-based policy = permissions that live on the resource itself**

---

## Why Resource-Based Policies Exist

Identity-based policies answer:
- What can *this identity* do?

Resource-based policies answer:
- Who can access *this resource*?

They exist to:
- Enable secure cross-account access
- Simplify service permissions
- Centralize control at the resource level

---

## Common AWS Services That Use Resource Policies

You will see resource-based policies in:

- Amazon S3 (Bucket Policies)
- AWS Lambda (Function Policies)
- Amazon SQS (Queue Policies)
- Amazon SNS (Topic Policies)
- AWS KMS (Key Policies)

👉 S3 bucket policies are the **most common** example.

---

## Identity-Based vs Resource-Based Policies

| Feature | Identity-Based Policy | Resource-Based Policy |
|------|----------------------|----------------------|
| Attached to | User / Role / Group | Resource |
| Defines | What identity can do | Who can access resource |
| Cross-account | Limited | Yes |
| Common use | General access | Shared resources |

👉 Both are evaluated together.

---

## S3 Bucket Policy (Most Important Example)

An S3 bucket policy:
- Is attached to a bucket
- Controls access to objects in that bucket
- Can allow access from other accounts

Example use cases:
- Allow CloudFront access
- Share bucket with another AWS account
- Enforce encryption or HTTPS

---

## Example: Cross-Account S3 Access (Conceptual)

Scenario:
- Account A owns the S3 bucket
- Account B needs read access

Solution:
- Add bucket policy in Account A
- Allow Account B principal
- Restrict actions and resources

👉 No IAM user sharing required.

---

## Lambda Resource Policies

Lambda uses resource-based policies to:
- Allow API Gateway to invoke a function
- Allow S3 or EventBridge triggers
- Enable cross-account invocation

Without this policy:
- Invocation will fail even if IAM allows it

---

## KMS Key Policies (Special Case)

KMS keys:
- Always use resource-based policies
- IAM policies alone are not enough

Key policies define:
- Who can use the key
- Who can manage the key

👉 KMS security depends heavily on key policies.

---

## Policy Evaluation (Important)

When accessing a resource:
1. Identity-based policies are evaluated
2. Resource-based policies are evaluated
3. Explicit deny always wins

Access is allowed only if:
- There is an explicit allow
- No explicit deny exists

---

## Common Beginner Mistakes

- Forgetting resource policies exist
- Allowing public access accidentally (S3)
- Assuming IAM policy alone is enough
- Over-permissive principals

These mistakes cause:
- Data leaks
- Security incidents

---

## Interview Tip

If asked:
> “How do you allow cross-account access to S3?”

Strong answer:
> By using an S3 bucket policy that explicitly allows the external AWS account to access specific bucket resources.

This shows **real-world IAM understanding**.

---

## Key Takeaways

- Resource-based policies live on resources
- Enable cross-account access
- Common in S3, Lambda, SQS, SNS, KMS
- Evaluated together with IAM policies
- Critical for secure AWS architectures

---

📌 **Next:** IAM Best Practices and Common Pitfalls
