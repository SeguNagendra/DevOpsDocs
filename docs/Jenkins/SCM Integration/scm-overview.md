---
sidebar_position: 1
---

# SCM Integration – Overview

This section covers **how Jenkins integrates with Source Control Management (SCM)** systems.
Correct SCM setup is foundational for reliable CI/CD, multibranch pipelines, and secure automation.

---

## Why SCM Integration Matters

SCM integration enables:
- Automated triggers on code changes
- Branch and PR discovery
- Pipeline-as-Code via Jenkinsfile
- Traceability between commits and builds

Poor SCM integration leads to:
- Missed builds
- Duplicate jobs
- Security risks
- Fragile pipelines

---

## Supported SCM Systems

Jenkins commonly integrates with:
- GitHub
- GitHub Enterprise
- GitLab
- Bitbucket
- Generic Git servers

> Git-based workflows are the industry standard.

---

## Core SCM Concepts in Jenkins

- **Repository**: Source code location
- **Credentials**: Secure access to SCM
- **Webhooks**: Event-driven triggers
- **Polling**: Fallback trigger mechanism
- **Branch indexing**: Discovery for multibranch pipelines

---

## Pipeline-as-Code with SCM

- Jenkinsfile lives in the repository
- SCM is the single source of truth
- Changes are versioned and reviewable
- Rollbacks are simple

---

## SCM Triggers

Common trigger mechanisms:
- Webhooks (recommended)
- Periodic polling (use cautiously)
- Manual triggers

Webhooks are preferred for:
- Faster feedback
- Lower Jenkins load

---

## Security Considerations

- Use tokens or SSH keys (not passwords)
- Scope credentials per repo or folder
- Restrict webhook secrets
- Limit who can configure SCM jobs

---

## Common Mistakes

- Using polling instead of webhooks by default
- Overusing global credentials
- Missing Jenkinsfile in repo
- Hardcoding branch names

---

## What This Section Covers

This section is split into focused documents:

- Git credentials & access methods
- Webhooks setup
- Multibranch SCM behavior
- Polling vs webhooks
- Common SCM integration failures

