---
sidebar_position: 1
---

# Credentials & Secrets Management – Overview

This section explains **how Jenkins securely handles secrets** such as passwords, tokens, and keys.
Incorrect credential handling is one of the **most serious security risks** in CI/CD pipelines.

---

## Why Credentials Management Matters

Poor credential practices lead to:
- Secret leaks in logs
- Compromised repositories
- Unauthorized access to environments
- Compliance violations

> Credentials must **never** be hardcoded in pipelines.

---

## What Are Jenkins Credentials?

Jenkins credentials are **securely stored secrets** managed by Jenkins and injected into pipelines only when needed.

Examples:
- Git credentials
- API tokens
- SSH private keys
- Username/password pairs
- Certificates

---

## How Jenkins Stores Credentials

- Encrypted at rest
- Stored in Jenkins credential store
- Accessible only via Jenkins APIs
- Never exposed in plain text

> Jenkins controls access using permissions and scopes.

---

## Credential Scope

Credentials can be scoped to:
- Global (available to all jobs)
- Folder (recommended for environments)
- Job (rarely recommended)

---

## Core Concepts Covered in This Section

This section is split into focused documents:

- Credential types
- Credentials binding
- `withCredentials` usage
- Security best practices
- Common mistakes and leaks

Each topic is covered **independently and practically**.

---

## Typical Real-World Use Cases

- Authenticating to Git repositories
- Accessing cloud APIs
- Deploying to servers via SSH
- Calling secured REST APIs

---

## Common Beginner Mistakes

- Hardcoding secrets in Jenkinsfile
- Echoing secrets in logs
- Passing secrets as parameters
- Overusing global credentials

---

## Interview Perspective

- Credential handling questions are common
- Expect security-focused scenarios
- Knowing `withCredentials` is mandatory