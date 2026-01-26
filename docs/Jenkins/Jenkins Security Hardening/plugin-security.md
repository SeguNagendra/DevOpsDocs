---
sidebar_position: 6
---

# Plugin Security

Plugins extend Jenkins functionality but also **extend its attack surface**.
Most serious Jenkins vulnerabilities originate from plugins.

---

## Why Plugin Security Is High Risk

Plugins:
- Run inside the controller JVM
- Often execute with high privileges
- Can access credentials, jobs, and agents

A vulnerable plugin can compromise the entire system.

---

## Plugin Trust Model

Important facts:
- Plugins are **not sandboxed**
- Plugin code is trusted by Jenkins
- One malicious plugin = full Jenkins access

Treat plugins like production code dependencies.

---

## Plugin Installation Rules

Only install plugins that:
- Are actively maintained
- Have a clear use case
- Are widely adopted

Avoid experimental or abandoned plugins.

---

## Plugin Update Strategy

Rules:
- Keep plugins updated
- Follow Jenkins security advisories
- Test updates in non-prod Jenkins
- Avoid mass upgrades blindly

Security patches often ship via plugins.

---

## Plugin Compatibility

- Plugins depend on Jenkins core versions
- Incompatible plugins cause instability
- Use dependency checks before upgrades

Never upgrade core or plugins in isolation.

---

## Reducing Plugin Attack Surface

Best practices:
- Minimize plugin count
- Remove unused plugins
- Disable risky plugins
- Avoid script-heavy plugins

Less plugins = less risk.

---

## Dangerous Plugin Patterns

High-risk behaviors:
- Arbitrary Groovy execution
- Custom authentication logic
- Direct filesystem access
- Network calls without validation

Review plugins carefully.

---

## Plugin Permissions & RBAC

- Restrict who can install plugins
- Limit admin access
- Audit plugin configuration changes

Never allow developers to self-install plugins.

---

## Monitoring Plugin Security

- Subscribe to Jenkins security advisories
- Track CVEs
- Monitor unusual Jenkins behavior after installs

---

## Common Plugin Security Failures

- Too many plugins installed
- No update process
- Unused legacy plugins
- Granting plugin install rights widely

---

## Best Practices

- Minimal plugin set
- Regular security reviews
- Staged rollout of updates
- Backup before plugin upgrades

---

## Interview Focus Areas

- Why plugins are dangerous
- Plugin vs Jenkins core security
- How to reduce plugin risk

