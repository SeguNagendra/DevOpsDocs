---
sidebar_position: 1
---

# Jenkins Pipeline – Overview

This section introduces **Jenkins Pipelines**, the core of modern Jenkins usage.
Pipelines define **how CI/CD flows are implemented as code**.

---

## What Is a Jenkins Pipeline?

A Jenkins Pipeline is a **series of automated steps** written in code that:
- Builds applications
- Runs tests
- Performs validations
- Deploys artifacts

Pipelines are defined using a **Jenkinsfile** stored in source control.

---

## Why Pipelines Matter

Pipelines solve problems that older job types could not:

- UI-based configuration drift
- Poor visibility into changes
- Lack of reusability
- Weak scalability

With pipelines, you get:
- Pipeline as Code
- Version control
- Reviewable changes
- Reusable logic
- Consistent execution

---

## Declarative vs Scripted Pipelines

Jenkins supports two pipeline syntaxes:

### Declarative Pipeline
- Structured and opinionated
- Easier to read
- Safer defaults
- Recommended for most teams

### Scripted Pipeline
- Fully Groovy-based
- Very flexible
- Harder to maintain
- Used only for advanced cases

> Always start with **Declarative**.

---

## What This Section Covers

You will learn:
- Jenkinsfile structure
- Stages vs steps
- Agent directive
- Environment and tools
- Basic pipeline control concepts

Each topic is documented **in its own file**.

---

## Common Beginner Mistakes

- Writing pipeline logic in UI
- Mixing scripted logic unnecessarily
- Hardcoding environment values
- Ignoring pipeline readability

---

## Interview Perspective

- Pipeline knowledge is mandatory
- Expect questions on Jenkinsfile structure
- Declarative vs Scripted comparison is common