---
sidebar_position: 2
title: IAM Users and Groups
---

# IAM Users and Groups

IAM Users and Groups are used to **manage human access** to AWS.
They help you control **who can log in** and **what actions they can perform**.

A clean user & group design is essential for:
- Security
- Auditing
- Easy permission management

---

## IAM Users (Deep Understanding)

An IAM user represents:
- A real person (developer, admin, auditor)
- Or a legacy application (not recommended)

Each IAM user can have:
- AWS Management Console access
- Programmatic access (access keys)

👉 **One IAM user = one person** (best practice).

---

## When to Use IAM Users

IAM users are suitable for:
- Human administrators
- Developers accessing AWS Console
- Short-term learning or labs

But:
- IAM users are **not ideal for applications**
- Long-term credentials are risky

👉 Prefer **IAM roles** for applications.

---

## IAM Groups (Why They Matter)

IAM Groups:
- Are collections of users
- Cannot log in themselves
- Have permissions attached via policies

Groups make permission management:
- Simple
- Consistent
- Scalable

---

## How Groups Are Used in Real Projects

Typical group structure:
- Admins → Full access
- Developers → Limited service access
- ReadOnly → Audit and view access

Users inherit permissions **from groups**.

👉 Avoid attaching policies directly to users.

---

## Example: Clean IAM Design

Instead of:
- Assigning permissions to 50 users individually

Do this:
- Create 3 groups
- Attach policies to groups
- Add users to groups

This design:
- Reduces errors
- Improves security
- Simplifies audits

---

## IAM Password Policy (Important)

AWS allows you to enforce:
- Minimum password length
- Complexity requirements
- Password rotation

Always:
- Enable a strong password policy
- Enforce MFA

---

## MFA for IAM Users (Mandatory)

Multi-Factor Authentication (MFA):
- Adds an extra security layer
- Protects against credential theft

Best practice:
- Enable MFA for **all IAM users**
- Mandatory for admins

---

## Programmatic Access & Access Keys

Access keys:
- Should be used carefully
- Must never be shared or committed to code

Best practice:
- Use roles instead of access keys
- Rotate keys if used

---

## Common Beginner Mistakes

- Sharing IAM users
- Giving AdminAccess to everyone
- Not using groups
- Ignoring MFA
- Hardcoding access keys

These mistakes cause:
- Security breaches
- Compliance failures

---

## Interview Tip

If asked:
> “How do you manage user access in AWS?”

Strong answer:
> By creating IAM users for individuals, grouping them using IAM groups, attaching policies to groups, and enforcing MFA.

This shows **real-world IAM understanding**.

---

## Key Takeaways

- IAM users represent people
- Groups simplify permission management
- Attach policies to groups, not users
- Enforce MFA and strong password policies
- Prefer roles for applications

---

📌 **Next:** IAM Roles
