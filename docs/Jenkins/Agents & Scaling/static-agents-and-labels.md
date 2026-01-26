---
sidebar_position: 2
---

# Static Agents & Labels

This document covers **static Jenkins agents** and **label-based scheduling**.
These are the foundation of most Jenkins installations before moving to Docker or Kubernetes.

---

## What Is a Static Agent?

A static agent is a **long-lived machine** registered with the Jenkins controller.

Common forms:
- VM
- Bare metal server
- Cloud instance (always on)

They are manually managed and persist across builds.

---

## When Static Agents Make Sense

Static agents are suitable when:
- Workloads are predictable
- Tooling is heavy (IDEs, browsers, SDKs)
- Infrastructure changes are rare
- Teams are small to medium

---

## Registering a Static Agent (High-Level)

Typical steps:
1. Create agent node in Jenkins
2. Assign labels
3. Configure executors
4. Connect agent (SSH / JNLP)
5. Verify online status

---

## Labels in Jenkins

Labels are **logical tags** assigned to agents.

Examples:
- `linux`
- `windows`
- `docker`
- `ui-tests`
- `java17`

Labels control **where a job runs**.

---

## Using Labels in Pipelines

```groovy
pipeline {
  agent { label 'linux && docker' }
  stages {
    stage('Build') {
      steps {
        sh 'mvn clean package'
      }
    }
  }
}
```

This runs only on agents matching **both** labels.

---

## Multiple Labels per Agent

An agent can have multiple labels:
```
linux docker java17 ui-tests
```

This allows flexible scheduling without duplicating agents.

---

## Label Expressions

Supported operators:
- `&&` (AND)
- `||` (OR)
- `!`  (NOT)

Example:
```groovy
agent { label 'linux && !gpu' }
```

---

## Executors on Static Agents

- Executors define parallel capacity
- Too many executors cause contention
- 1–2 executors per CPU-heavy agent is common

Avoid using static agents as build farms.

---

## Common Mistakes

- Overloading one static agent
- Too many executors
- Poor label naming
- Running heavy builds on controller

---

## Best Practices

- Use clear, capability-based labels
- Keep executors low
- Isolate heavy workloads
- Plan migration to ephemeral agents

---

## Interview Focus Areas

- What labels do
- How Jenkins selects an agent
- Executors vs agents

