---
sidebar_position: 14
---

# Security & Access Management – Users, Roles, and Tokens

As SonarQube becomes part of daily development and CI/CD pipelines,
**security and access control** become extremely important.

This chapter explains how SonarQube manages users, permissions, and security-related workflows
in a clear and practical way.

---

## Why Security Matters in SonarQube

SonarQube has access to:
- Source code structure
- Security findings
- CI/CD credentials (via tokens)
- Organization-wide quality rules

Poor access control can lead to:
- Unauthorized scans
- Leaked tokens
- Accidental configuration changes

Security should be treated as a **first-class concern**.

---

## Users in SonarQube

SonarQube supports different types of users:
- Administrators
- Developers
- Viewers

Users can authenticate via:
- Local accounts
- LDAP
- SSO (in enterprise setups)

Each user should have **only the permissions they need**.

---

## Global vs Project-Level Permissions

SonarQube separates permissions into two levels.

### Global Permissions
Control access to:
- System administration
- Quality Profiles
- Quality Gates
- Global settings

Only a small number of trusted users should have global permissions.

---

### Project-Level Permissions
Control access to:
- Viewing project data
- Running analyses
- Browsing and resolving issues

Most developers only need project-level permissions.

---

## Roles and Their Responsibilities

Typical roles include:
- **Admin** – Full control
- **Developer** – Analyze code, fix issues
- **Viewer** – Read-only access

Clearly defining roles prevents confusion and accidental changes.

---

## Authentication Tokens

Tokens are the preferred authentication method for:
- CI/CD pipelines
- Automation tools
- Scanners

Best practices:
- One token per pipeline or tool
- Never reuse personal tokens
- Rotate tokens periodically
- Revoke unused tokens

Tokens should always be treated as secrets.

---

## Security Hotspots Workflow

Security hotspots represent:
- Sensitive code areas
- Potential security risks
- Areas requiring human judgment

Workflow:
1. SonarQube flags a hotspot
2. Developer reviews the code
3. Hotspot is marked safe or unsafe
4. Action is documented

This ensures security decisions are **intentional and auditable**.

---

## Common Security Mistakes

Avoid these issues:
- Giving admin access to everyone
- Hardcoding tokens in pipelines
- Ignoring security hotspots
- Sharing tokens across teams

Small mistakes can have large consequences.

---

## Best Practices

Follow these guidelines:
- Apply least-privilege access
- Audit permissions regularly
- Educate developers on security findings
- Treat SonarQube as a shared platform

Good governance builds trust and adoption.

---

## Key Takeaway

Strong security and access control:
- Protects the platform
- Prevents misuse
- Supports scalable adoption

Security in SonarQube is about **control, not restriction**.

---

➡️ **Next:** Governance & Enterprise Usage  
