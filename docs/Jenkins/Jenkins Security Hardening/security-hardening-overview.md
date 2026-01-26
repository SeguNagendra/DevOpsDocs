---
sidebar_position: 1
---

# Jenkins Security Hardening – Overview

This section focuses on **securing Jenkins controllers, agents, pipelines, and integrations**.
Security hardening is critical once Jenkins is used by multiple teams or exposed to networks.

---

## Why Jenkins Security Matters

An insecure Jenkins setup can lead to:
- Source code leaks
- Credential compromise
- Production access breaches
- Full infrastructure takeover

Jenkins often has **very high privileges**, making it a prime attack target.

---

## Jenkins Threat Model (High-Level)

Common attack surfaces:
- Web UI (authentication & authorization)
- Credentials store
- Build agents executing untrusted code
- Plugins with high privileges
- SCM webhooks and integrations

Security must be layered.

---

## Core Security Areas

This section covers security across:

- Authentication & Authorization (RBAC)
- Controller hardening
- Agent trust & isolation
- Credential protection
- Plugin security
- Network exposure
- Audit & monitoring

---

## Principle of Least Privilege

Apply least privilege to:
- Users
- Agents
- Credentials
- Plugins

Never assume Jenkins users are fully trusted.

---

## Built-in Security Features

Jenkins provides:
- Matrix-based security
- Role-based authorization (plugin)
- Credentials masking
- CSRF protection
- Script security sandbox

These must be **explicitly configured**.

---

## Common Real-World Security Failures

- Anonymous access enabled
- Controller running builds
- Over-privileged agents
- Global admin for all users
- Unreviewed plugin installs

---

## Security vs Usability

Good security:
- Enables safe self-service
- Protects production
- Scales across teams

Bad security:
- Blocks delivery
- Encourages bypasses

Balance is required.

---

## What This Section Covers

This section is split into focused documents:

- Authentication & Authorization
- Role-based access control
- Controller hardening
- Agent security & isolation
- Plugin security
- Network & ingress security
- Auditing and monitoring

---

## Interview Focus Areas

- Jenkins threat model
- RBAC vs matrix security
- Why controller isolation matters

