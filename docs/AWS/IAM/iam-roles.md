---
sidebar_position: 3
title: IAM Roles
---

# IAM Roles

IAM Roles are **the most important and most used IAM concept** in AWS.
Modern AWS architectures rely on roles **instead of long-term credentials**.

If users answer IAM questions confidently,
👉 it’s usually because they understand **IAM Roles well**.

---

## What Is an IAM Role? (Simple Explanation)

An IAM Role:
- Is an AWS identity with permissions
- Does **not** have long-term credentials
- Is assumed temporarily by trusted entities

In simple terms:
> **IAM Role = temporary permissions, assumed when needed**

---

## Why IAM Roles Exist

Problems with access keys:
- Can be leaked
- Can be hardcoded
- Are difficult to rotate

IAM Roles solve this by:
- Providing temporary credentials
- Automatically rotating credentials
- Eliminating secret management

👉 Roles are **far more secure than users**.

---

## Who Can Assume a Role?

Roles can be assumed by:
- AWS services (EC2, Lambda, ECS)
- IAM users
- Other AWS accounts
- Identity providers (SSO, AD)

This is controlled by the **trust policy**.

---

## IAM Role Components

Every IAM role has **two key policies**:

### 1. Trust Policy
- Defines **who can assume the role**
- Uses `sts:AssumeRole`

### 2. Permission Policy
- Defines **what the role can do**
- Same policy syntax as users

👉 Both are required for a role to work.

---

## IAM Roles for AWS Services (Very Important)

Most AWS services use roles.

Examples:
- EC2 → Access S3, CloudWatch
- Lambda → Access DynamoDB
- ECS → Pull images, write logs

Roles allow services to:
- Access AWS APIs securely
- Without storing credentials

---

## Example: EC2 Role (Conceptual)

Typical EC2 role usage:
1. Create IAM role
2. Attach permissions (e.g., S3 read access)
3. Attach role to EC2 instance
4. EC2 accesses S3 automatically

👉 No access keys needed.

---

## Cross-Account Access Using Roles

IAM Roles enable:
- Secure cross-account access
- No need to share credentials

Flow:
- Account A creates role
- Account B assumes role
- Temporary credentials issued

Used heavily in:
- Multi-account AWS setups
- Enterprise organizations

---

## Role Session Duration

- Roles are temporary
- Session duration can be configured
- Shorter sessions = better security

---

## Common Beginner Mistakes

- Using access keys instead of roles
- Confusing trust policy with permission policy
- Over-permissioning roles
- Attaching roles incorrectly

These mistakes cause:
- Security risks
- Access failures

---

## Interview Tip

If asked:
> “How do EC2 instances access AWS services securely?”

Strong answer:
> By using IAM roles attached to EC2 instances, which provide temporary credentials without hardcoding secrets.

This shows **production-grade IAM knowledge**.

---

## Key Takeaways

- IAM roles provide temporary credentials
- Preferred over users and access keys
- Used by AWS services and applications
- Enable cross-account access
- Core to secure AWS architectures

---

📌 **Next:** IAM Policies
