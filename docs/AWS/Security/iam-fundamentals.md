---
sidebar_position: 2
title: IAM Fundamentals
---

# IAM Fundamentals

Identity and Access Management (IAM) is the **core security service** in AWS.
Almost every security incident in AWS traces back to **IAM misconfiguration**.

Before advanced security services,
👉 you must deeply understand **IAM fundamentals**.

---

## What Is IAM? (Simple Explanation)

AWS IAM allows you to:
- Create identities (users, roles)
- Define permissions (policies)
- Control access to AWS resources

In simple terms:
> **IAM = who can do what on which AWS resource**

---

## Why IAM Is So Important

IAM controls:
- Access to AWS services
- Access to data
- Access between services

Poor IAM design leads to:
- Data breaches
- Accidental deletions
- Privilege escalation

👉 IAM is the **first and strongest line of defense**.

---

## Core IAM Components

IAM is built on four main components:

1. Users  
2. Groups  
3. Roles  
4. Policies  

Understanding how these work together is critical.

---

## IAM Users

IAM users:
- Represent a human or application
- Have long-term credentials
- Can log in to AWS console or API

Best practices:
- Avoid creating many users
- Prefer roles over users
- Never share users

---

## IAM Groups

IAM groups:
- Collection of users
- Used to assign permissions easily

Example:
- Developers group
- Admins group
- ReadOnly group

👉 Permissions are assigned to groups, not individual users.

---

## IAM Roles (Very Important)

IAM roles:
- Do not have long-term credentials
- Are assumed temporarily
- Used by AWS services and applications

Common use cases:
- EC2 accessing S3
- Lambda accessing DynamoDB
- Cross-account access

👉 **Roles are the preferred way to grant access in AWS**.

---

## IAM Policies

Policies define:
- What actions are allowed or denied
- On which resources
- Under what conditions

Policies are written in JSON.

Two main types:
- AWS-managed policies
- Customer-managed policies

---

## How Permissions Work

Permissions are evaluated using:
- Identity-based policies
- Resource-based policies
- Explicit deny always wins

Rule:
> **If it’s not explicitly allowed, it’s denied**

---

## Least Privilege Principle

Least privilege means:
- Grant only required permissions
- Nothing more

Benefits:
- Reduced attack surface
- Lower blast radius
- Safer environments

---

## IAM Root Account (Critical)

Root account:
- Has full access
- Cannot be restricted by IAM

Best practices:
- Enable MFA
- Do not use root for daily tasks
- Lock away root credentials

---

## IAM Credentials

IAM supports:
- Passwords (console access)
- Access keys (programmatic access)

Best practices:
- Rotate access keys
- Avoid hardcoding credentials
- Use roles instead

---

## IAM Policy Evaluation Logic

Order of evaluation:
1. Explicit deny
2. Explicit allow
3. Default deny

Understanding this prevents permission confusion.

---

## Common Beginner Mistakes

- Using root account daily
- Attaching AdministratorAccess everywhere
- Hardcoding access keys
- Ignoring least privilege

These mistakes cause:
- Major security incidents

---

## Interview Tip

If asked:
> “How do you control access in AWS?”

Strong answer:
> By using IAM users and roles with least privilege policies, preferring roles over long-term credentials.

---

## Key Takeaways

- IAM controls access to AWS
- Roles are preferred over users
- Policies define permissions
- Least privilege is mandatory
- Root account must be protected

---

📌 **Next:** IAM Policies Deep Dive
