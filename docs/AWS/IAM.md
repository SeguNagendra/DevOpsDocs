---
sidebar_position: 3
---

## AWS IAM (Identity and Access Management) – Complete Notes

## 1. Why IAM Exists (Real-World Analogy)

### Bank Example
Think of *AWS Account = Bank Building*

Inside the bank:
- Service Desk
- Employee Desk
- Debit / Credit Section
- Vault

Not everyone can access everything.

### Two Core Questions:
1. *Who are you?* → Authentication  
2. *What are you allowed to do?* → Authorization  

---

## 2. Authentication vs Authorization

### Authentication
Verifies *identity*.
Examples:
- Username & Password
- Access Key & Secret Key
- MFA

### Authorization
Verifies *permissions*.
Examples:
- Can you read S3?
- Can you delete EC2?

---

## 3. Why AWS Introduced IAM

Without IAM:
- Everyone uses root account
- Anyone can delete resources

With IAM:
- Controlled access
- Least privilege
- Secure operations

---

## 4. What is AWS IAM?

AWS IAM is a *global AWS service* that manages:
- Users
- Permissions
- Secure access

✔ Manage who can access AWS

✔ Control what actions they can perform

✔ Define which resources they can access

✔ Enforce least privilege security

IAM is *free* and *region-independent*.

---

## 5. Core IAM Components

IAM has four main components:
1. Users
2. Groups
3. Policies
4. Roles

---

## 6. IAM Users

An IAM User represents:
- A human (Dev, QA, Admin)
- Rarely a service

A user only provides *authentication*.
Without policies → user can do nothing.

### Access Types:
- Console Access
- Programmatic Access

---

## 7. IAM Policies

Policies define *what actions are allowed or denied*.

### Sample Policy:
```json
{
  "Effect": "Allow",
  "Action": "s3:GetObject",
  "Resource": "arn:aws:s3:::my-bucket/*"
}
```

### Policy Types:
- AWS Managed
- Customer Managed (recommended)
- Inline

---

## 8. IAM Groups

Groups simplify permission management.

### Example Groups:
- Developers
- QA
- DBAdmins
- Admins

Best practice:
- Attach policies to groups
- Add users to groups

---

## 9. IAM Roles

Roles:
- Are not users
- Provide temporary credentials
- Used by applications and AWS services

Roles rely on *STS*.

---

## 10. Role Use Cases

### EC2 Accessing S3
- EC2 assumes role
- Role has S3 permissions

### On-Prem App Accessing AWS
- App assumes role
- No IAM user created

### Cross-Account Access
- One account assumes role in another

---

## 11. Temporary Credentials (STS)

- Short-lived
- Secure
- Auto-rotated

---

## 12. Root Account Best Practices

- Do not use daily
- Enable MFA
- Never share credentials

---

## 13. IAM Best Practices

- Enable MFA
- Use least privilege
- Prefer roles over users
- Avoid inline policies
- Rotate access keys
- Monitor using CloudTrail

---

## 14. IAM Summary

| Component | Purpose |
|--------|--------|
| User | Identity |
| Policy | Permission |
| Group | Permission management |
| Role | Temporary access |

---

## 15. Bank vs AWS Mapping

| Bank Concept | AWS IAM |
|------------|--------|
| Entry Gate | Authentication |
| Security Desk | Authorization |
| Employee ID | IAM User |
| Access Card | Policy |
| Department | Group |
| Temporary Pass | Role |

---

## 16. Common Interview Traps

- IAM is regional ❌
- Roles use access keys ❌
- Root should be used daily ❌

---

## 17. Final Notes

IAM ensures *secure, scalable, and controlled access* to AWS resources.
Mastering IAM is critical for *real-world AWS projects and interviews*