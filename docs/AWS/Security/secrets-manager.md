---
sidebar_position: 7
title: AWS Secrets Manager
---

# AWS Secrets Manager

Hardcoding passwords and API keys is one of the **most common security mistakes**.
AWS Secrets Manager exists to **securely store, manage, and rotate secrets**.

Secrets Manager is a **critical service for production security**.

---

## What Is AWS Secrets Manager? (Simple Explanation)

AWS Secrets Manager:
- Stores secrets securely
- Encrypts secrets using KMS
- Controls access using IAM
- Supports automatic rotation

In simple terms:
> **Secrets Manager = secure vault for sensitive information**

---

## What Are Secrets?

Secrets include:
- Database passwords
- API keys
- OAuth tokens
- Application credentials

These must:
- Never be hardcoded
- Never be stored in plaintext

---

## Why Secrets Manager Exists

Without Secrets Manager:
- Credentials are hardcoded
- Rotation is manual
- Breaches go unnoticed

Secrets Manager provides:
- Centralized secret storage
- Automatic rotation
- Fine-grained access control
- Audit logs

---

## How Secrets Manager Works

High-level flow:
1. Secret is stored encrypted with KMS
2. IAM controls who can access it
3. Applications retrieve secrets securely
4. Rotation updates secrets automatically

👉 Secrets are decrypted **only at access time**.

---

## Secrets Manager vs Parameter Store

| Feature | Secrets Manager | Parameter Store |
|------|-----------------|-----------------|
| Encryption | Yes (KMS) | Yes (KMS) |
| Rotation | Automatic | Manual |
| Cost | Paid | Mostly free |
| Use case | Credentials | Config values |

👉 Use Secrets Manager for **passwords and keys**.

---

## Automatic Secret Rotation

Secrets Manager supports:
- Automatic rotation using Lambda
- Built-in templates for RDS

Rotation process:
- Generate new secret
- Update service
- Validate access
- Remove old secret

👉 Rotation reduces credential exposure.

---

## Accessing Secrets Securely

Applications access secrets using:
- IAM roles
- AWS SDK

Best practice:
- Use roles, not access keys
- Restrict access to specific secrets

---

## Security Best Practices

- Use customer-managed KMS keys
- Restrict IAM permissions
- Enable rotation
- Monitor access via CloudTrail

---

## Common Beginner Mistakes

- Hardcoding secrets
- Storing secrets in environment variables forever
- Overly broad IAM permissions
- No rotation enabled

These mistakes cause:
- Credential leaks

---

## Interview Tip

If asked:
> “How do you manage secrets in AWS?”

Strong answer:
> By using AWS Secrets Manager to securely store and rotate credentials encrypted with KMS.

---

## Key Takeaways

- Secrets Manager stores sensitive data securely
- Integrates with KMS and IAM
- Supports automatic rotation
- Preferred over hardcoding secrets
- Essential for production security

---

📌 **Next:** AWS Certificate Manager (ACM)
