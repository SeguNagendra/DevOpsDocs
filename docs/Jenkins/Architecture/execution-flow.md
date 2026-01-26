---
sidebar_position: 7
---

# Jenkins Execution Flow

This document explains the **end-to-end lifecycle of a Jenkins build**.
Understanding this flow helps you debug delays, failures, and resource issues.

---

## High-Level Execution Flow

A Jenkins build follows this sequence:

1. Trigger
2. Controller receives request
3. Job enters queue
4. Agent selection
5. Executor allocation
6. Workspace creation
7. Build execution
8. Result collection

Every Jenkins feature maps back to this flow.

---

## Step-by-Step Execution Lifecycle

### 1. Build Triggered
A build can be triggered by:
- SCM webhook
- Manual trigger
- CRON schedule
- Upstream job
- API call

---

### 2. Controller Receives the Event
- Controller validates job configuration
- Evaluates parameters and conditions
- Places job into the queue

---

### 3. Job Enters the Queue
The job waits in the queue when:
- No agents are available
- Executors are busy
- Label constraints are unmet
- Locks or throttles are active

---

### 4. Agent Selection
Controller selects an agent based on:
- Node labels
- Availability
- Executor count
- Resource constraints

---

### 5. Executor Allocation
- One executor is assigned
- Job leaves the queue
- Execution begins

---

### 6. Workspace Creation
- Workspace directory is created on the agent
- Source code is checked out
- Environment variables are set

---

### 7. Build Execution
- Pipeline stages execute sequentially or in parallel
- Tools and scripts run on the agent
- Logs stream back to the controller

---

### 8. Result & Post Actions
- Build status is determined (SUCCESS / FAILURE / UNSTABLE)
- Post steps run
- Artifacts may be archived
- Notifications sent

---

## Parallel & Matrix Execution

- Parallel stages consume multiple executors
- Matrix builds create multiple execution paths
- Resource availability determines speed

---

## Failure Scenarios & Behavior

### Agent Goes Offline
- Build pauses or fails
- Job may re-enter queue

### Controller Restart
- Running builds stop
- Pipeline may resume if durability is enabled

---

## Where Common Issues Occur

| Stage | Common Problem |
|------|---------------|
| Queue | Jobs stuck |
| Agent | Offline nodes |
| Executor | Resource starvation |
| Workspace | Disk issues |
| Execution | Test failures |

---

## Interview Traps

- **Where does execution happen?**  
  → On agents

- **Who controls scheduling?**  
  → Controller

- **Can Jenkins resume builds?**  
  → Yes, if configured

---

## Key Takeaways

- Controller orchestrates
- Agents execute
- Executors control parallelism
- Queue explains delays