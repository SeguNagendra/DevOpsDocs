---
sidebar_position: 5
---

# Agent Directive

The `agent` directive defines **where a pipeline or stage runs**.
Misusing agents is a common cause of unstable and slow Jenkins pipelines.

---

## What Is the Agent Directive?

The `agent` directive tells Jenkins:
- Which node/agent to use
- Where commands should execute
- How resources are allocated

Without an agent, a pipeline **cannot run**.

---

## Global Agent

A global agent applies to **all stages** in the pipeline.

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

### Common Global Agent Options
- `any` → any available agent
- `none` → no global agent (must define per stage)
- `label` → specific agent

---

## Stage-Level Agent

Stage-level agents override the global agent.

```groovy
pipeline {
  agent none
  stages {
    stage('Linux Tests') {
      agent { label 'linux' }
      steps {
        sh 'run-tests.sh'
      }
    }
  }
}
```

### When to Use Stage-Level Agents
- Different OS requirements
- Different tools per stage
- Isolating heavy workloads

---

## Agent with Labels

Labels allow targeting specific agents.

```groovy
agent { label 'docker && linux' }
```

### Common Use Cases
- Browser-specific testing
- OS-specific builds
- Resource-heavy jobs

---

## Docker Agents (High-Level)

Pipelines can run inside Docker containers:

```groovy
agent {
  docker {
    image 'maven:3.9-eclipse-temurin-17'
  }
}
```

Benefits:
- Clean environments
- Tool consistency
- Isolation

---

## agent none (Important)

```groovy
agent none
```

Used when:
- You want full control
- Each stage needs a different agent
- Avoids unnecessary workspace creation

---

## Common Mistakes

- Running everything on `agent any`
- Forgetting `agent none` when using stage agents
- Running heavy jobs on controller
- Overusing executors on one agent

---

## Best Practices

- Use `agent any` for simple pipelines
- Use `agent none` + stage-level agents for complex flows
- Isolate heavy jobs using labels
- Prefer more agents over more executors

---

## Interview Traps

- **Is agent mandatory?**  
  → Yes

- **Can stages override global agent?**  
  → Yes

- **Where does execution happen?**  
  → On the selected agent
