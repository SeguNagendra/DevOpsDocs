---
sidebar_position: 8
title: IAM Real-World Scenarios
---

# IAM Real-World Scenarios

Understanding IAM concepts is important, but **using IAM correctly in real projects** is what truly matters.
This page walks through **common real-world IAM scenarios** that every AWS / DevOps engineer encounters.

These scenarios appear in:
- Daily production work
- System design interviews
- Security reviews

---

## Scenario 1: EC2 Accessing S3 Securely

### Problem
An EC2 instance needs to:
- Read files from an S3 bucket
- Without storing access keys

### Correct Solution
- Create an IAM Role
- Attach S3 read permissions
- Attach role to EC2 instance

### Why This Works
- Uses temporary credentials
- No secrets stored on disk
- Automatically rotated

👉 **This is the correct and expected AWS design**.

---

## Scenario 2: Lambda Accessing DynamoDB

### Problem
A Lambda function needs to:
- Read and write DynamoDB data

### Correct Solution
- Create an IAM role for Lambda
- Attach DynamoDB permissions
- Lambda assumes the role automatically

### Common Mistake
- Using access keys in environment variables ❌

---

## Scenario 3: Cross-Account Access (CI/CD)

### Problem
A CI/CD pipeline in Account A needs to:
- Deploy resources in Account B

### Correct Solution
- Create IAM role in Account B
- Allow Account A to assume role
- Use `sts:AssumeRole`

### Why This Is Secure
- No credential sharing
- Clear audit trail
- Temporary access

---

## Scenario 4: Restricting Admin Actions with MFA

### Problem
Admins should:
- Use MFA for sensitive actions
- Avoid accidental changes

### Correct Solution
- Use IAM policy conditions
- Require `aws:MultiFactorAuthPresent = true`

This is **mandatory in real enterprises**.

---

## Scenario 5: S3 Bucket Shared with Another Account

### Problem
Another AWS account needs:
- Read-only access to your S3 bucket

### Correct Solution
- Use S3 bucket policy
- Allow external account principal
- Restrict actions and resources

Never:
- Create IAM users for other accounts ❌

---

## Scenario 6: Temporary Access for Contractors

### Problem
A contractor needs:
- Temporary access for 2 weeks

### Correct Solution
- Use IAM role with limited permissions
- Set session duration
- Enforce MFA

Avoid:
- Permanent IAM users ❌

---

## Scenario 7: Blocking Access from Unapproved Regions

### Problem
Compliance requires:
- Resource creation only in approved regions

### Correct Solution
- Use IAM policy conditions
- Restrict `aws:RequestedRegion`

This helps:
- Cost control
- Compliance

---

## Common IAM Anti-Patterns (Avoid These)

- Hardcoded access keys
- Shared IAM users
- Overuse of AdministratorAccess
- No MFA
- No auditing

These lead to **security incidents**.

---

## Interview Tip

If asked:
> “How do you design IAM for production?”

Strong answer:
> By using IAM roles for services, enforcing least privilege with policies and conditions, enabling MFA, and avoiding long-term credentials.

This signals **real production experience**.

---

## Key Takeaways

- IAM roles solve most real-world problems
- Temporary credentials are safer
- Resource-based policies enable sharing
- Conditions enforce security boundaries
- Correct IAM design prevents incidents

---

📌 **Next:** IAM Review and Summary
