---
sidebar_position: 2
---

# Authentication & Authorization

This document explains **how Jenkins identifies users (authentication)** and **controls what they can do (authorization)**.
Getting this wrong is one of the fastest ways to compromise a Jenkins environment.

---

## Authentication vs Authorization

- **Authentication**: Who are you?
- **Authorization**: What are you allowed to do?

Both must be configured. Authentication alone is not security.

---

## Authentication Methods

### Jenkins Internal User Database
- Users managed directly in Jenkins
- Simple to set up
- Not recommended for large teams

**Use when**:
- Small teams
- Temporary setups
- Local labs

---

### LDAP / Active Directory
- Centralized identity management
- Enterprise standard
- Supports groups

**Recommended for**:
- Corporate environments
- On‑prem Jenkins

---

### SSO / Identity Providers (OIDC, SAML)
- GitHub, GitLab, Azure AD, Okta, Google
- Modern and secure
- Best user experience

**Recommended for**:
- Cloud Jenkins
- Multi-team environments

---

## Authentication Best Practices

- Disable anonymous access
- Enforce strong passwords (if local users)
- Prefer SSO or LDAP
- Rotate service account credentials
- Enable MFA at IdP level

---

## Authorization Models

Authorization determines **permissions after login**.

### Matrix-Based Security
- Built-in
- Fine-grained permissions
- Hard to manage at scale

---

### Role-Based Authorization (Plugin)
- Define roles (admin, dev, viewer)
- Assign users/groups to roles
- Scales much better

**Recommended for production Jenkins**.

---

## Permission Categories

Common permission groups:
- Overall (admin, read)
- Job (build, configure)
- Run (replay, update)
- Credentials (use, configure)
- Agent (connect, configure)

Avoid granting broad permissions.

---

## Service Accounts

Use service accounts for:
- Automation
- SCM webhooks
- API access

Rules:
- No UI login
- Minimal permissions
- Token-based auth only

---

## Common Misconfigurations

- Anonymous read access enabled
- Everyone is admin
- Mixing human and service accounts
- No separation between prod and non-prod

---

## Best Practices

- Centralize identity (SSO / LDAP)
- Use RBAC plugin
- Grant least privilege
- Separate human and machine identities
- Review permissions periodically

---

## Interview Focus Areas

- Authentication vs authorization
- Matrix vs RBAC
- Why anonymous access is dangerous
- Service account best practices

