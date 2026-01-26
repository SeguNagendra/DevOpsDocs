---
sidebar_position: 6
---

# Workspace & Queue

This document explains **where Jenkins stores files** and **why builds wait before execution**.
These concepts are critical for debugging stuck or flaky pipelines.

---

## Jenkins Workspace

### What Is a Workspace?

A **workspace** is a directory on an **agent** where Jenkins:
- Checks out source code
- Executes build steps
- Stores temporary build artifacts

> Workspaces are **agent-specific**, not controller-based.

---

## Workspace Location

- Each job has its own workspace directory
- Multibranch pipelines create separate workspaces per branch
- Parallel stages create isolated workspace instances

Typical path:
```
$JENKINS_HOME/workspace/<job-name>
```

(Note: This path exists **on the agent**, not controller)

---

## Workspace Lifecycle

1. Workspace is created on agent
2. Code is checked out
3. Build steps execute
4. Workspace may be reused or cleaned
5. Job completes

---

## Common Workspace Problems

- Dirty workspace causing flaky tests
- Old binaries reused accidentally
- Disk space exhaustion
- Conflicts between parallel builds

### Best Practices
- Clean workspace when required
- Avoid sharing workspace between jobs
- Use stash/unstash for data transfer

---

## Jenkins Queue

### What Is the Queue?

The **queue** holds jobs waiting for execution.

Jobs enter the queue when:
- Triggered manually or automatically
- No agent is available
- No executor is free
- Label constraints are unmet

---

## Why Jobs Stay in Queue

Common reasons:
- Agents offline
- All executors busy
- Label mismatch
- Throttling rules
- Locked resources

---

## Queue Ownership

- Queue is managed entirely by the **controller**
- Agents never manage the queue

---

## Diagnosing Queue Issues

Check:
- Node status
- Executor availability
- Job labels
- Throttle & lock rules

---

## Interview Traps

- **Where is workspace created?**  
  → On the agent

- **Who manages the queue?**  
  → Controller

- **Can multiple builds share a workspace?**  
  → No (unless misconfigured)