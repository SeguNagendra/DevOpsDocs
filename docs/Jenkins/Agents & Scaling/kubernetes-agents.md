---
sidebar_position: 5
---

# Kubernetes Agents

Kubernetes agents allow Jenkins to run builds as **ephemeral pods** inside a Kubernetes cluster.
This is the **most scalable and cloud-native Jenkins execution model**.

---

## What Is a Kubernetes Agent?

A Kubernetes agent is a **temporary pod** created on demand for a Jenkins build.

Key traits:
- One pod per build (usually)
- Destroyed after completion
- Fully isolated environment
- Defined via pod templates

---

## Why Kubernetes Agents Are Used

Kubernetes agents solve problems such as:
- Static agent saturation
- Tool version conflicts
- Inefficient scaling
- Costly idle infrastructure

They enable **true horizontal auto-scaling**.

---

## High-Level Architecture

1. Jenkins controller runs outside or inside Kubernetes
2. Kubernetes plugin requests a pod
3. Kubernetes schedules the pod
4. Pipeline runs inside the pod
5. Pod is destroyed after completion

---

## Pod Templates

Pod templates define:
- Containers
- Images
- Resources (CPU / memory)
- Volumes
- Environment variables

They act as **agent blueprints**.

---

## Basic Declarative Example

```groovy
pipeline {
  agent {
    kubernetes {
      label 'maven-agent'
      defaultContainer 'maven'
      yaml '''
apiVersion: v1
kind: Pod
spec:
  containers:
  - name: maven
    image: maven:3.9-eclipse-temurin-17
    command:
    - cat
    tty: true
'''
    }
  }
  stages {
    stage('Build') {
      steps {
        sh 'mvn clean package'
      }
    }
  }
}
```

---

## Multi-Container Pods

Common pattern:
- One container for build
- One for tools (Docker, scanners)

Example:
- `maven`
- `docker`
- `kubectl`

---

## Resource Management

Always define:
- CPU requests/limits
- Memory requests/limits

This prevents:
- Node exhaustion
- Unstable clusters

---

## Kubernetes Agents vs Docker Agents

| Aspect | Docker Agents | Kubernetes Agents |
|------|---------------|-------------------|
| Isolation | Container | Pod (multi-container) |
| Scaling | Limited | Auto-scaled |
| Infra | VM-based | Cloud-native |
| Cost efficiency | Medium | High |
| Enterprise adoption | Medium | High |

---

## Common Mistakes

- No resource limits
- Large pod templates
- Too many containers per pod
- Running Jenkins controller with build permissions

---

## Best Practices

- Use small, purpose-built images
- One pod per pipeline
- Define resource requests and limits
- Separate prod and non-prod clusters
- Restrict pod permissions

---

## Security Considerations

- Pods execute untrusted code
- Use Kubernetes RBAC
- Avoid privileged containers
- Isolate namespaces

---

## Interview Focus Areas

- Docker agents vs Kubernetes agents
- Why pods are preferred over containers
- Pod templates and lifecycle

