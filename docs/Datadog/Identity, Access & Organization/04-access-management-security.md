---
sidebar_position: 2
---

# Access Management & Security (RBAC)

> *“Good observability without access control becomes a security risk.”*

This module belongs to **PHASE 2: Identity, Access & Organization**.  
Here, we focus on **who can do what** inside Datadog — and why that matters.

---

## Why Access Management Matters

As Datadog adoption grows:
- More teams use the platform
- More dashboards and monitors exist
- More sensitive production data is visible

Without proper access control:
- Anyone can change alerts
- Dashboards get overwritten
- Security and compliance risks increase

---

## Users in Datadog

A **user** represents a real person or system interacting with Datadog.

Users can:
- View dashboards
- Create monitors
- Manage configurations (depending on role)

Best practice:
> One Datadog user per real person  
> Avoid shared human accounts

---

## Roles in Datadog (RBAC)

Datadog uses **Role-Based Access Control (RBAC)**.

A **role** defines:
- What actions are allowed
- Which resources can be accessed

Examples:
- Read-only user
- Standard user
- Admin
- Custom roles

Roles are **assigned to users**, not resources.

---

## Permissions Model (Conceptual)

Permissions control actions such as:
- Creating or editing monitors
- Modifying dashboards
- Managing integrations
- Viewing sensitive data

Good RBAC design:
- Follows least privilege
- Starts restrictive
- Expands only when required

---

## API Keys vs Application Keys

This is a **very common interview topic**.

### API Key
- Identifies your Datadog organization
- Used to send data *into* Datadog
- Should be treated as sensitive

### Application Key
- Represents a user or service
- Used to interact with Datadog APIs
- Scoped by permissions

Simple rule:
> API key = who you are  
> App key = what you can do

---

## Service Accounts

Service accounts are used by:
- CI/CD pipelines
- Automation tools
- Terraform
- Scripts

Best practices:
- Use service accounts instead of personal users
- Assign minimal roles
- Rotate keys regularly

---

## Single Sign-On (SSO) – High Level

Datadog supports SSO via:
- SAML
- Identity providers (Okta, Azure AD, etc.)

Benefits:
- Centralized identity management
- Easier onboarding/offboarding
- Improved security posture

SSO is recommended for:
> Medium to large organizations

---

## Common Access Control Mistakes

❌ Everyone is admin  
❌ Shared admin accounts  
❌ Long-lived API keys  
❌ No audit visibility  

---

## Why This Module Matters

Strong access management:
- Protects production visibility
- Reduces accidental changes
- Supports compliance needs
- Scales with teams

Weak access management:
- Causes outages
- Creates audit gaps
- Slows incident response

---

## Key Takeaways

- RBAC controls who can do what
- Use least privilege
- Separate human users and service accounts
- Protect API and application keys
- SSO improves security and scale

---

➡️ **Next Module:** Datadog Agent Architecture
