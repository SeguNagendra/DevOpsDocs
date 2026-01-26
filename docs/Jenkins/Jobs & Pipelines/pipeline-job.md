---
sidebar_position: 3
---

# Pipeline Job

Pipeline jobs are the **standard and recommended way** to use Jenkins today.
They enable **Pipeline as Code**, scalability, and clean CI/CD design.

---

## What Is a Pipeline Job?

A Pipeline job defines the entire build logic using a **Jenkinsfile** written in code.

Key characteristics:
- Stored in source control
- Versioned and reviewable
- Reproducible across environments
- Supports complex workflows

---

## Pipeline as Code (Why It Matters)

Using code instead of UI configuration provides:
- Change history
- Code reviews
- Rollback capability
- Team collaboration
- Reduced configuration drift

> Modern Jenkins = Pipeline Job + Jenkinsfile

---

## Where Pipeline Logic Lives

- Jenkinsfile resides in SCM (Git)
- Jenkins UI only references the repository
- Pipeline behavior is driven entirely by code

---

## Types of Pipelines

### Declarative Pipeline
- Structured and opinionated
- Easier to read and maintain
- Recommended for most teams

### Scripted Pipeline
- More flexible
- Groovy-based
- Used for advanced scenarios

> Learn Declarative first.

---

## High-Level Pipeline Structure

```groovy
pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'mvn clean install'
      }
    }
  }
}
```

---

## Why Pipeline Jobs Scale Better

- Native support for parallel execution
- Works with shared libraries
- Handles retries, timeouts, approvals
- Integrates well with SCM and cloud

---

## Pipeline Job vs Freestyle

| Feature | Pipeline Job | Freestyle Job |
|-------|--------------|---------------|
| Stored as code | ✅ | ❌ |
| Version control | ✅ | ❌ |
| Parallel stages | ✅ | ❌ |
| Shared libraries | ✅ | ❌ |
| Modern CI/CD | ✅ | ❌ |

---

## Common Mistakes

- Writing all logic in UI instead of Jenkinsfile
- Hardcoding credentials
- Overusing scripted pipelines

---

## Interview Perspective

- Pipeline jobs are expected knowledge
- Explain Pipeline as Code clearly
- Know Declarative vs Scripted difference
