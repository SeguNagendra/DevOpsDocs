---
sidebar_position: 3
---

# Jenkins Controller (Master)

This document focuses on the **Jenkins Controller**, its internals, and its role in build orchestration.
Understanding this helps prevent unstable Jenkins setups and production outages.

---

## What Is the Jenkins Controller?

The Jenkins Controller (formerly Master) is the **brain of Jenkins**.
It coordinates all activities but should avoid heavy execution work.

---

## Core Responsibilities

The controller is responsible for:

- Hosting Jenkins UI and REST APIs
- Storing job and pipeline configurations
- Managing plugins and extensions
- Receiving SCM events (webhooks, polling)
- Scheduling jobs
- Managing the build queue
- Allocating executors on agents
- Tracking build states and results

---

## What the Controller Does NOT Do

The controller must **not**:

- Run CPU-intensive builds
- Execute Selenium/UI tests
- Perform Docker builds (in prod setups)
- Hold large workspaces

> Keeping the controller lightweight is critical for stability.

---

## Controller Internals

### JENKINS_HOME
- Stores Jenkins configuration
- Contains job definitions
- Holds plugin data
- Persists build metadata

### Jobs & Pipelines
- Job configs are stored as XML
- Pipelines are executed from Jenkinsfiles
- Multibranch pipelines dynamically create jobs

---

## Queue Management

- All jobs enter the **queue** first
- Jobs wait when:
  - No agents are available
  - Executors are exhausted
  - Label constraints are not met

### Queue Is Managed Only by the Controller

---

## Scheduling Logic

The controller decides:
- Which agent can run the job
- When an executor is free
- Whether constraints are satisfied

Scheduling considers:
- Node labels
- Executor count
- Throttling rules
- Lockable resources

---

## Failure Scenarios

### If Controller Goes Down
- UI becomes unavailable
- No new jobs can start
- Running jobs may fail or hang

### If Controller Is Overloaded
- Slow UI
- Delayed scheduling
- Random build failures

---

## Security Responsibilities

- User authentication
- Authorization & roles
- Credential storage (encrypted)
- CSRF protection

---

## Production Best Practices

- Dedicated VM/Pod for controller
- Regular backups of JENKINS_HOME
- Minimal plugin installation
- No build execution on controller
- Monitor CPU, memory, disk usage

---

## Interview Traps

- **Does the controller execute builds?**  
  → No (except in non-prod or misconfigured setups)

- **Where is the queue managed?**  
  → On the controller

- **What happens if controller restarts?**  
  → Builds stop; configuration persists
