---
sidebar_position: 4
---

# Jenkins Agent (Slave / Node)

This document explains **Jenkins Agents**, which are responsible for executing builds and tests.
Agents do the real work in Jenkins.

---

## What Is a Jenkins Agent?

A Jenkins Agent (formerly Slave) is a machine or container that:
- Executes pipeline stages
- Runs builds and tests
- Hosts required tools
- Manages workspaces

Agents are controlled by the Jenkins **Controller**.

---

## Agent Responsibilities

An agent is responsible for:

- Running build steps
- Executing test automation
- Creating and managing workspaces
- Hosting tools (Java, Maven, Node, Docker, browsers)
- Sending build results back to the controller

---

## Agent Types

### Static Agents
- Permanently available machines
- Preconfigured with tools
- Suitable for stable workloads

### Dynamic Agents
- Created on demand
- Short-lived
- Common in Docker/Kubernetes setups

---

## Agent Connectivity Methods

### SSH Agents
- Controller connects to agent via SSH
- Most common setup
- Preferred for Linux agents

### JNLP Agents
- Agent initiates outbound connection
- Useful behind firewalls
- Requires Java on agent

---

## Executors on Agents

- Executors define how many jobs an agent can run in parallel
- Configured per agent
- More executors = more resource usage

### Best Practice
- Start with 1–2 executors per agent
- Scale agents horizontally instead of increasing executors

---

## Node Labels

- Labels are used to target specific agents
- Common use cases:
  - OS-specific builds
  - Browser-specific testing
  - Heavy vs lightweight jobs

### Example
```groovy
agent { label 'linux && docker' }
```

---

## Workspace on Agents

- Workspaces are created on agents
- Each job and branch has its own workspace
- Parallel builds use separate workspace directories

### Common Problems
- Dirty workspaces
- Disk space exhaustion
- Tool version conflicts

---

## Scaling Strategies

- Prefer more agents over more executors
- Use labels to isolate workloads
- Use dynamic agents for burst workloads

---

## Security Best Practices

- Agents should have minimal permissions
- Do not store secrets on agents
- Use Jenkins credentials binding
- Isolate agents by purpose

---

## Interview Traps

- **Where does execution happen?**  
  → On agents

- **Can agents run without controller?**  
  → No

- **Is it safe to run builds on controller?**  
  → No, not in production
