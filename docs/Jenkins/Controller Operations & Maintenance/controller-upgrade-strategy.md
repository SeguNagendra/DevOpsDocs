---
sidebar_position: 2
---

# Controller Upgrade Strategy

Upgrading the Jenkins controller is one of the **highest-risk operational tasks**.
A disciplined upgrade strategy prevents outages, data loss, and long recovery windows.

---

## Why Jenkins Upgrades Fail

Common causes:
- Plugin incompatibilities
- Skipping multiple core versions
- No rollback plan
- No test environment
- Upgrading during business hours

Most failures are preventable.

---

## Jenkins Release Types

### LTS (Recommended)
- Released every 12 weeks
- Backported security fixes
- Stable and predictable

### Weekly
- Faster feature delivery
- Higher risk
- Not recommended for production

Always use **LTS for production controllers**.

---

## Pre-Upgrade Checklist

Before upgrading:
- Review Jenkins LTS changelog
- Review plugin compatibility
- Take full backups
- Freeze config changes
- Notify stakeholders
- Ensure rollback path exists

Never upgrade blindly.

---

## Plugin Compatibility Strategy

Rules:
- Update plugins **before** core upgrade
- Remove unused plugins
- Check plugin minimum core requirements
- Avoid mass plugin upgrades

Plugins break upgrades more than core.

---

## Upgrade Paths

Recommended:
- Incremental LTS upgrades
- Avoid skipping major LTS lines

Example:
```
2.387.x → 2.401.x → 2.414.x
```

---

## Test Environment Strategy

Always have:
- Non-prod Jenkins
- Same plugins and config
- Same authentication setup

Test upgrades there first.

---

## Upgrade Execution Steps (High-Level)

1. Put Jenkins in quiet mode
2. Take final backup
3. Upgrade Jenkins core
4. Verify startup
5. Validate critical jobs
6. Monitor logs closely

---

## Rollback Strategy

Rollback options:
- Restore from backup
- Revert container image
- Roll back VM snapshot

If rollback is hard, upgrade is unsafe.

---

## Post-Upgrade Validation

Validate:
- UI access
- Authentication & RBAC
- Agent connectivity
- Pipeline execution
- Plugin functionality

---

## Common Upgrade Mistakes

- Upgrading core and plugins together
- No backup before upgrade
- Ignoring deprecation warnings
- No rollback testing

---

## Best Practices

- LTS only
- Small, frequent upgrades
- Document upgrade steps
- Automate Jenkins deployments
- Treat upgrades as routine

---

## Interview Focus Areas

- LTS vs weekly releases
- Plugin vs core upgrade order
- Safe rollback strategies

