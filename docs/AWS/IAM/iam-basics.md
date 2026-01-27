---
sidebar_position: 1
title: IAM Basics
---

# AWS IAM – Basics

IAM (Identity and Access Management) is **the most critical security service in AWS**.

If networking controls **where traffic can go**,
👉 IAM controls **who can do what in AWS**.

Misconfigured IAM is the **#1 cause of AWS security incidents**.

---

## What Is IAM? (Simple Explanation)

AWS IAM allows you to:
- Create identities (users, roles)
- Grant permissions
- Control access to AWS resources

In simple terms:
> **IAM = authentication + authorization for AWS**

---

## Why IAM Exists

Without IAM:
- Everyone would have full access
- No accountability
- No security boundaries

IAM exists to:
- Enforce least privilege
- Track actions (audit)
- Secure AWS environments

👉 IAM is the foundation of AWS security.

---

## Core IAM Concepts (Must Know)

You must clearly understand these building blocks:

- Users
- Groups
- Roles
- Policies

We will cover each **in detail** next.

---

## IAM Users

An IAM user:
- Represents a **person or application**
- Has long-term credentials
- Can be assigned permissions

Best practices:
- One user per person
- Avoid sharing users

⚠️ IAM users should be used **sparingly**.

---

## IAM Groups

IAM groups:
- Are collections of users
- Have policies attached
- Simplify permission management

Example:
- Admins group
- Developers group
- ReadOnly group

👉 Assign permissions to groups, not users.

---

## IAM Roles

IAM roles:
- Are assumed temporarily
- Do NOT have long-term credentials
- Are used by AWS services and apps

Used by:
- EC2
- Lambda
- ECS
- Cross-account access

👉 Roles are **preferred over users**.

---

## IAM Policies

Policies define:
- What actions are allowed or denied
- On which resources
- Under what conditions

Policies are written in **JSON**.

IAM permissions = **policy-based**.

---

## Authentication vs Authorization

- Authentication: Who are you?
- Authorization: What can you do?

IAM handles **both**.

---

## IAM Is Global (Important)

IAM:
- Is global (not region-specific)
- Applies across all AWS regions

👉 One IAM configuration affects the entire account.

---

## Common Beginner Mistakes

- Using root account for daily work
- Creating too many IAM users
- Granting AdministratorAccess everywhere
- Hardcoding credentials

These mistakes cause:
- Security breaches
- Compliance failures

---

## Interview Tip

If asked:
> “What is IAM?”

Strong answer:
> IAM is a global AWS service used to manage identities and control access to AWS resources using policies.

Short, accurate, professional.

---

## Key Takeaways

- IAM controls access in AWS
- Users, groups, roles, policies are core components
- Roles are preferred over users
- Least privilege is critical
- Foundation of AWS security

---

📌 **Next:** IAM Users and Groups
