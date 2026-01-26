---
sidebar_position: 4
---

# Docker Agents

Docker agents allow Jenkins to run builds inside **ephemeral containers**.
They solve tool conflicts, environment drift, and scalability issues seen with static agents.

---

## What Is a Docker Agent?

A Docker agent runs pipeline steps inside a Docker container instead of directly on the host agent.

Key characteristics:
- Short-lived (ephemeral)
- Clean environment per build
- Defined by an image

---

## Why Use Docker Agents

Docker agents help when:
- Different projects need different tool versions
- Builds pollute static agents
- Reproducibility is required
- Scaling demand is bursty

---

## How Docker Agents Work

High-level flow:
1. Jenkins schedules a build
2. Docker plugin pulls image (if needed)
3. Container is started
4. Pipeline runs inside container
5. Container is destroyed

---

## Using Docker Agent in Declarative Pipeline

```groovy
pipeline {
  agent {
    docker {
      image 'maven:3.9-eclipse-temurin-17'
      args '-v /var/run/docker.sock:/var/run/docker.sock'
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

## Stage-Level Docker Agent

```groovy
pipeline {
  agent none
  stages {
    stage('Test') {
      agent {
        docker { image 'node:20' }
      }
      steps {
        sh 'npm test'
      }
    }
  }
}
```

Use this to mix environments in one pipeline.

---

## Docker Agent vs Static Agent

| Aspect | Static Agent | Docker Agent |
|------|-------------|--------------|
| Environment | Persistent | Ephemeral |
| Isolation | Low | High |
| Tool conflicts | Common | Eliminated |
| Startup time | Fast | Slightly slower |
| Scaling | Manual | Easier |

---

## Workspace Behavior

- Workspace is mounted into container
- Files persist for the duration of the build
- Stash/unstash still works normally

---

## Common Mistakes

- Running Docker-in-Docker unnecessarily
- Huge base images
- No image pinning (`latest`)
- Mounting too many host volumes

---

## Best Practices

- Pin image versions
- Keep images small
- Use stage-level Docker agents when possible
- Prefer Docker agents over static tool installs

---

## Security Considerations

- Docker socket access = root-level risk
- Restrict who can use Docker agents
- Use dedicated Docker-capable agents
- Avoid running untrusted code with host mounts

---

## Interview Focus Areas

- Docker agent vs Kubernetes agent
- Stage-level vs pipeline-level Docker agent
- Workspace behavior inside containers

