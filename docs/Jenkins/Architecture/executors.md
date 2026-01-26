---
sidebar_position: 5
---

# Jenkins Executors

Executors control **how many jobs run in parallel** in Jenkins.  
Misunderstanding executors is a common cause of **overloaded agents and flaky builds**.

---

## What Is an Executor?

An **executor** is a single slot on an agent that can execute **one job at a time**.

- Executors belong to **agents**, not jobs
- Each running build consumes **one executor**
- Executors directly impact CPU, memory, and disk usage

---

## Executors vs Agents

| Concept | Purpose |
|------|--------|
| Agent | Machine/container that runs jobs |
| Executor | Parallel execution slot on an agent |

> One agent can have multiple executors.

---

## How Executors Work

- Job enters queue
- Controller finds a matching agent
- Controller checks available executors
- Executor is allocated
- Job starts execution

If no executor is free → job waits in queue.

---

## Configuring Executors

- Executors are configured **per agent**
- Default executor count is often **2**
- Controller also has executors (should be set to 0 in prod)

### Best Practice
- Set controller executors to **0**
- Use agents for execution

---

## Parallelism Strategies

### Option 1: Increase Executors (Not Recommended)
- Higher CPU & memory contention
- Risk of flaky tests

### Option 2: Add More Agents (Recommended)
- Better isolation
- Horizontal scaling
- More stable builds

---

## Executors & Pipelines

In pipelines:
- Each stage may consume an executor
- Parallel stages consume multiple executors simultaneously

### Example
```groovy
parallel {
  stage('Chrome') { steps { sh 'run-tests.sh' } }
  stage('Edge') { steps { sh 'run-tests.sh' } }
}
```

This requires **2 free executors**.

---

## Common Misconfigurations

- Too many executors on a small agent
- Running heavy jobs in parallel on same agent
- Not accounting for memory-intensive tests

---

## Monitoring Executors

Watch for:
- Long queue times
- Agent CPU spikes
- Out-of-memory errors

These usually indicate executor misconfiguration.

---

## Interview Traps

- **Does each stage need an executor?**  
  → Yes, when it executes steps

- **Where are executors configured?**  
  → On agents

- **Should controller have executors?**  
  → No, not in production
