---
sidebar_position: 5
---

# Jenkins Plugin Strategy

Plugins are the **power and the biggest risk** in Jenkins.
A bad plugin strategy is the #1 reason Jenkins becomes unstable over time.

---

## Why Plugin Strategy Matters

Problems caused by poor plugin management:
- Jenkins startup failures
- Random build breakages
- Security vulnerabilities
- Upgrade nightmares

> More plugins ≠ better Jenkins

---

## Jenkins Plugin Model (Quick Overview)

- Jenkins core provides minimal functionality
- Almost everything else comes from plugins
- Plugins run inside the controller JVM

This means:
- Plugins directly affect controller stability
- Plugin bugs can crash Jenkins

---

## Core Plugins (Essential)

These are commonly required in almost all setups:

- Pipeline
- Git
- Credentials Binding
- SSH Agent
- Workspace Cleanup
- JUnit (for test reports)

> Install only what you actively use.

---

## Optional / Use-Case Plugins

Install only when required:

- HTML Publisher (reports)
- Email Extension
- Docker Pipeline
- Kubernetes
- Lockable Resources
- Throttle Concurrent Builds

---

## Plugins You Should Be Careful With

- Old / unmaintained plugins
- Plugins with low adoption
- UI-only plugins with no real value
- Plugins that duplicate core features

Always check:
- Last update date
- Active maintainers
- Compatibility with your Jenkins version

---

## Plugin Installation Best Practices

- Prefer Jenkins LTS
- Install plugins incrementally
- Restart Jenkins after plugin install
- Avoid installing plugins directly on prod first
- Test plugin changes in lower environments

---

## Plugin Upgrade Strategy

- Never auto-upgrade plugins blindly
- Upgrade plugins in batches
- Read changelogs before upgrading
- Backup JENKINS_HOME before upgrades

---

## Removing Plugins Safely

- Disable plugin first
- Observe system behavior
- Remove only if safe
- Restart Jenkins

---

## Security Considerations

- Plugins can introduce vulnerabilities
- Regularly check security advisories
- Remove unused plugins

---

## Common Mistakes

- Installing “Suggested Plugins” blindly
- Too many overlapping plugins
- Ignoring plugin updates for years

---

## Interview Traps

- **Do plugins run on controller or agent?**  
  → Controller

- **Can a plugin crash Jenkins?**  
  → Yes

- **Is Jenkins usable without plugins?**  
  → Barely
