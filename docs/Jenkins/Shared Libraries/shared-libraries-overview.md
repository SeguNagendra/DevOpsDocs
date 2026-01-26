---
sidebar_position: 1
---

# Shared Libraries – Overview

This section covers **Jenkins Shared Libraries**, the standard way to reuse pipeline logic across jobs.
They are essential for **scalable, maintainable CI/CD** in real projects.

---

## Why Shared Libraries Matter

Without shared libraries:
- Pipelines become large and duplicated
- Changes must be copied across repos
- Bugs multiply
- Governance is impossible

Shared libraries enable:
- Reuse of pipeline logic
- Centralized fixes
- Consistent standards
- Cleaner Jenkinsfiles

---

## What Is a Jenkins Shared Library?

A shared library is a **versioned Git repository** containing reusable pipeline code that Jenkins can load.

It typically contains:
- Custom pipeline steps
- Helper functions
- Standardized workflows

---

## How Shared Libraries Are Used

In Jenkinsfiles:
```groovy
@Library('my-shared-lib') _
```

Once loaded, library functions are available to pipelines.

---

## Typical Use Cases

- Build and test wrappers
- Deployment logic
- Environment validation
- Notification handling
- Retry and error-handling logic

---

## Repository Structure (High-Level)

A shared library usually contains:
- `vars/` → Global pipeline steps
- `src/` → Groovy classes
- `resources/` → Templates/files

Structure is strict and important.

---

## Versioning Strategy

- Use Git tags or branches
- Pin versions for stability
- Avoid using `master/main` blindly

---

## Security Considerations

- Shared libraries execute Groovy code
- Treat them as trusted code
- Restrict who can modify them
- Review changes carefully

---

## Common Mistakes

- Duplicating logic instead of sharing
- No version pinning
- Putting everything in Jenkinsfile
- Unreviewed changes to shared libs

---

## Interview Focus Areas

- Why shared libraries exist
- vars vs src differences
- How libraries are loaded and versioned

