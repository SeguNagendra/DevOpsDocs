---
sidebar_position: 4
---

# Security Incident Scenarios

This document covers **real-world Jenkins security incidents**,
how to recognize them quickly, and how to respond without making things worse.

---

## Scenario 1: Credential Leak in Build Logs

### Symptoms
- Secrets visible in console output
- Credentials exposed in archived logs

### Likely Causes
- Missing credential masking
- Echoing environment variables
- Poor pipeline design

### Immediate Actions
1. Revoke exposed credentials immediately
2. Remove affected build logs
3. Rotate dependent secrets

### Long-Term Fix
- Enforce credential binding
- Mask secrets by default
- Audit pipelines regularly

---

## Scenario 2: Unauthorized Admin Access

### Symptoms
- Unknown admin users
- Unexpected configuration changes

### Likely Causes
- Weak RBAC configuration
- Shared admin accounts
- Compromised credentials

### Immediate Actions
- Disable suspicious accounts
- Rotate admin credentials
- Review audit logs

### Long-Term Fix
- Enforce least privilege
- Enable SSO with MFA
- Audit admin access regularly

---

## Scenario 3: Malicious Jenkinsfile Changes

### Symptoms
- Unexpected commands executed
- Data exfiltration attempts

### Likely Causes
- Untrusted PRs running pipelines
- No sandboxing

### Immediate Actions
- Stop affected jobs
- Review SCM access logs
- Revoke compromised credentials

### Long-Term Fix
- Restrict PR execution
- Use trusted libraries
- Enforce review policies

---

## Scenario 4: Plugin Vulnerability Exploited

### Symptoms
- Security advisories triggered
- Unexpected controller behavior

### Likely Causes
- Outdated plugins
- No vulnerability scanning

### Immediate Actions
- Disable affected plugin
- Apply patches or rollback

### Long-Term Fix
- Regular plugin updates
- Plugin governance policies

---

## Scenario 5: Compromised Build Agent

### Symptoms
- Suspicious outbound traffic
- Altered build artifacts

### Likely Causes
- Shared agents
- Persistent workspaces
- Unpatched OS

### Immediate Actions
- Terminate agent
- Rotate credentials
- Inspect produced artifacts

### Long-Term Fix
- Use ephemeral agents
- Harden agent images
- Isolate networks

---

## Security Incident Playbook

Always:
- Contain first
- Rotate secrets
- Preserve evidence
- Communicate clearly

---

## How Interviewers Evaluate Security Scenarios

They look for:
- Fast containment
- Least-privilege mindset
- Understanding Jenkins as an attack surface

---

## Interview Focus Areas

- Secret handling mistakes
- PR security risks
- Plugin vulnerability response

