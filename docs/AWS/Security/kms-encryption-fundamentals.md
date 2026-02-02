---
sidebar_position: 6
title: KMS Encryption Fundamentals
---

# AWS KMS – Encryption Fundamentals

Encryption is a **non-negotiable requirement** in modern cloud systems.
AWS Key Management Service (KMS) is the **central service for managing encryption keys** in AWS.

Before using encrypted S3 buckets or RDS encryption,
👉 you must understand **how KMS actually works**.

---

## What Is AWS KMS? (Simple Explanation)

AWS KMS is a managed service that:
- Creates and manages encryption keys
- Controls who can use keys
- Integrates with AWS services for encryption

In simple terms:
> **KMS = secure service to manage encryption keys**

---

## Why KMS Exists

Without KMS:
- Keys would be hardcoded
- Key rotation would be manual
- Auditing key usage would be difficult

KMS provides:
- Secure key storage
- Access control via IAM
- Automatic key rotation
- Audit logging

---

## Encryption Basics (Quick Refresher)

### Encryption at Rest
- Data is encrypted when stored

### Encryption in Transit
- Data is encrypted while moving

AWS supports both by default in many services.

---

## Customer Master Keys (CMK)

In KMS, encryption keys are called:
- **Customer Master Keys (CMKs)**

Types of CMKs:
- AWS-managed keys
- Customer-managed keys

👉 Customer-managed keys give **more control**.

---

## AWS-Managed vs Customer-Managed Keys

| Feature | AWS-Managed | Customer-Managed |
|------|------------|------------------|
| Creation | Automatic | User-controlled |
| Rotation | Automatic | Configurable |
| Policy control | Limited | Full |
| Use case | Simple encryption | Compliance & control |

---

## Envelope Encryption (Critical Concept)

KMS uses **envelope encryption**:

Process:
1. KMS generates a data key
2. Data key encrypts data
3. Data key is encrypted by CMK
4. Encrypted data key is stored

Benefits:
- Performance
- Scalability
- Security

👉 KMS never encrypts large data directly.

---

## Data Keys

Data keys:
- Are used to encrypt actual data
- Exist temporarily in memory
- Are destroyed after use

CMKs:
- Protect data keys

---

## Key Policies (Very Important)

Key policies:
- Control who can use a CMK
- Are mandatory for KMS keys

Think of key policies as:
> **IAM policies for encryption keys**

Without correct key policy:
- IAM permissions alone won’t work

---

## IAM vs Key Policy

For KMS access:
- IAM policy + Key policy are both required

Rule:
> **If key policy denies, access is denied**

---

## Key Rotation

Rotation options:
- Automatic (once per year)
- Manual

Best practice:
- Enable automatic rotation for CMKs

---

## KMS Integration with AWS Services

KMS integrates with:
- S3
- EBS
- RDS
- Lambda
- Secrets Manager

Encryption is often:
- Transparent
- Automatic

---

## Security and Compliance

KMS provides:
- FIPS 140-2 validated HSMs
- Audit logs via CloudTrail
- Fine-grained access control

Used for:
- PCI-DSS
- HIPAA
- ISO compliance

---

## Common Beginner Mistakes

- Using AWS-managed keys blindly
- Misconfiguring key policies
- Deleting keys accidentally
- Not enabling rotation

These mistakes cause:
- Data loss
- Access failures

---

## Interview Tip

If asked:
> “How does encryption work in AWS?”

Strong answer:
> By using AWS KMS with envelope encryption to manage and protect encryption keys.

---

## Key Takeaways

- KMS manages encryption keys
- Uses envelope encryption
- CMKs protect data keys
- Key policies are critical
- Integrated with most AWS services

---

📌 **Next:** AWS Secrets Manager
