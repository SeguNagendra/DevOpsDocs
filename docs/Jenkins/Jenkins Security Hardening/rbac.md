---
sidebar_position: 3
---

# Role-Based Access Control (RBAC)

RBAC is the **recommended authorization model** for production Jenkins.
It allows permissions to be managed at scale without turning Jenkins into an admin-only tool.

---

## Why RBAC Is Needed

Matrix-based security becomes unmanageable when:
- Teams grow
- Jobs increase
- Permissions differ by role

RBAC solves this by grouping permissions logically.

---

## RBAC Plugin Overview

Commonly used plugin:
- Role-based Authorization Strategy

It enables:
- Role definitions
- User/group assignments
- Folder-level access control

---

## Role Types

### Global Roles
- Admin
- Read-only
- Support

Control overall Jenkins access.

---

### Item (Job) Roles
- Job configuration
- Build permissions
- Read-only access

Applied to folders or jobs.

---

### Agent Roles
- Connect
- Configure
- Disconnect

Protects build infrastructure.

---

## Typical Role Design

Example roles:
- **Admin**: Full control
- **Developer**: Configure & run jobs
- **Viewer**: Read-only
- **Service Account**: Limited automation access

Keep roles minimal and purpose-driven.

---

## Folder-Based RBAC (Best Practice)

- Create folders per team or project
- Apply item roles at folder level
- Avoid job-level permission sprawl

This scales cleanly.

---

## Assigning Users & Groups

- Prefer groups over individual users
- Integrate with LDAP/SSO groups
- Avoid manual per-user assignments

---

## Least Privilege Enforcement

Rules:
- Grant minimum permissions
- Avoid global admin access
- Separate prod and non-prod roles

---

## Common RBAC Mistakes

- Too many global admins
- Assigning permissions directly to users
- No separation between environments
- Overlapping roles with unclear ownership

---

## RBAC Validation Checklist

- Can devs configure only their jobs?
- Are prod jobs restricted?
- Are service accounts isolated?
- Can agents be managed by non-admins?

---

## Interview Focus Areas

- RBAC vs Matrix security
- Why folder-level RBAC scales
- Common RBAC anti-patterns

