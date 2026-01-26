---
sidebar_position: 8
---

# Auditing & Monitoring

Auditing and monitoring help you **detect misuse, attacks, and misconfigurations** in Jenkins.
Security is incomplete without visibility.

---

## Why Auditing Matters

Without auditing:
- Breaches go unnoticed
- Misuse cannot be traced
- Compliance fails
- Incident response is slow

Logs are evidence.

---

## What Should Be Audited

Key areas to audit:
- User logins and failures
- Permission changes
- Job configuration changes
- Credential access and updates
- Plugin installs and updates
- Agent connections and disconnects

---

## Jenkins Audit Logs

Enable:
- Audit Trail plugin (or equivalent)
- System log recording
- Security-related event logging

Store logs **outside Jenkins**.

---

## Job & Configuration Changes

Track:
- Who changed what
- When it was changed
- What was modified

Folder-based RBAC improves audit clarity.

---

## Credential Usage Auditing

Monitor:
- Credential creation/deletion
- Scope changes
- Unexpected usage patterns

Rotate credentials after suspicious activity.

---

## Agent & Build Monitoring

Watch for:
- Unusual agent creation
- Long-running or stuck builds
- Sudden spike in build activity

These often indicate abuse.

---

## Plugin & System Monitoring

Track:
- Plugin installation events
- Jenkins restarts
- JVM memory and CPU usage

Unexpected changes require investigation.

---

## Centralized Logging

Recommended:
- Ship Jenkins logs to SIEM
- Correlate with SCM, cloud, and network logs
- Set alerts for high-risk events

Visibility must be centralized.

---

## Alerting Strategy

Alert on:
- Admin permission changes
- New plugins installed
- Jenkins exposed publicly
- Controller executor enabled
- Excessive login failures

Avoid alert fatigue.

---

## Compliance Considerations

Auditing supports:
- SOC2
- ISO 27001
- Internal security reviews

Retention policies matter.

---

## Common Auditing Failures

- Logs stored only on controller
- No alerting
- No retention policy
- No review process

Logs unused = logs useless.

---

## Best Practices

- Enable audit logging early
- Centralize and retain logs
- Review alerts regularly
- Test incident response

---

## Interview Focus Areas

- Why auditing is required
- What Jenkins events must be logged
- Difference between logging and monitoring

