---
sidebar_position: 3
---

# Executors – Deep Dive

Executors define **how much parallel work Jenkins can run**.
Misconfiguring executors is one of the **top causes of slow, unstable Jenkins systems**.

---

## What Is an Executor?

An executor represents **one execution slot** on an agent.

- 1 executor = 1 build step at a time
- Executors run pipelines, freestyle jobs, stages
- Executors consume CPU, memory, disk, and network

Executors do **not** create resources — they share existing ones.

---

## Controller Executors vs Agent Executors

### Controller Executors
- Should usually be set to **0**
- Running builds on controller causes:
  - UI slowness
  - Plugin instability
  - Jenkins crashes

### Agent Executors
- Where real work should run
- Must be sized carefully

---

## How Executors Affect Concurrency

If an agent has:
- 1 executor → 1 job at a time
- 4 executors → up to 4 concurrent jobs

More executors ≠ faster builds.

---

## Why Too Many Executors Is Bad

Too many executors cause:
- CPU contention
- Memory pressure
- Disk I/O bottlenecks
- Random build failures

This is especially bad for:
- UI tests
- Docker builds
- Heavy JVM workloads

---

## Executor Sizing Guidelines

General rules (not absolute):

| Workload Type | Executors |
|--------------|-----------|
| CPU-heavy (builds, tests) | 1–2 |
| IO-heavy | 2–4 |
| UI / Browser tests | 1 |
| Docker builds | 1 |

Always measure and adjust.

---

## Executors and Pipelines

- Pipelines consume executors at stage execution
- Idle stages do not consume executors
- `input` steps can block executors if not handled properly

---

## Queue vs Executors

- **Queue**: Waiting jobs
- **Executors**: Active jobs

A growing queue usually means:
- Too few agents
- Wrong labels
- Executors exhausted

---

## Common Misconfigurations

- High executor count on single agent
- Running builds on controller
- Same executor count for all agents
- Ignoring workload type

---

## Best Practices

- Set controller executors to 0
- Prefer more agents over more executors
- Isolate heavy workloads
- Monitor CPU, memory, disk
- Revisit executor count periodically

---

## Interview Focus Areas

- What an executor is
- Why controller executors are dangerous
- Executors vs agents
- Queue vs executor

