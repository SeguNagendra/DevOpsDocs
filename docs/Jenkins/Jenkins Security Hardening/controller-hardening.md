---
sidebar_position: 4
---

# Controller Hardening

The Jenkins controller is the **most sensitive component** in the system.
If compromised, attackers gain access to credentials, pipelines, agents, and infrastructure.

---

## Why Controller Hardening Is Critical

A hardened controller:
- Reduces blast radius
- Prevents privilege escalation
- Improves stability
- Limits attack surface

Most real-world Jenkins breaches start at the controller.

---

## Do Not Run Builds on Controller

Rule:
- Set controller executors to **0**

Why:
- Builds execute arbitrary code
- Plugins run in controller JVM
- Resource exhaustion risks

Controllers should orchestrate, not execute.

---

## Secure Jenkins Configuration

Key settings:
- Disable anonymous access
- Enable CSRF protection
- Use secure session cookies
- Enforce HTTPS

Never expose Jenkins over plain HTTP.

---

## Script Security & Groovy Sandbox

- Disable unsafe script approvals
- Review all approved scripts
- Prefer sandboxed pipelines

Groovy has full JVM access if unrestricted.

---

## Credentials Protection

- Minimize global credentials
- Restrict credential usage permissions
- Avoid exposing secrets to controller logs
- Rotate credentials regularly

---

## Plugin Hygiene

- Install only required plugins
- Remove unused plugins
- Keep plugins up to date
- Monitor plugin security advisories

Plugins run with controller privileges.

---

## JVM & OS Hardening

- Run Jenkins as non-root user
- Restrict filesystem permissions
- Limit outbound network access
- Use OS-level firewalls

---

## Backup & Recovery Readiness

- Regular backups
- Secure backup storage
- Test restore procedures

Hardening includes recovery.

---

## Common Hardening Failures

- Controller running builds
- Admin access for all users
- Old vulnerable plugins
- Publicly exposed Jenkins UI

---

## Hardening Checklist

- Controller executors = 0
- HTTPS enforced
- RBAC enabled
- Plugins minimal and updated
- Backups configured

---

## Interview Focus Areas

- Why controller is high-risk
- Controller vs agent responsibilities
- Plugin security risks

