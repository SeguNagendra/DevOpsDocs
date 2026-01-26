---
sidebar_position: 2
---

# Master–Slave Architecture (Controller–Agent)

This document explains the **core execution model of Jenkins**.  
Every pipeline, build, and job runs based on this architecture.

---

## Terminology Clarification

| Legacy Term | Current Term |
|------------|--------------|
| Master     | Controller   |
| Slave      | Agent / Node |

> Jenkins officially uses *Controller / Agent*, but *Master / Slave* is still widely referenced.

---

## What Is Master–Slave Architecture?

Jenkins uses a **distributed execution model** where:

- The **Controller** manages orchestration and scheduling
- The **Agents** perform the actual build and test execution

This separation ensures:
- Scalability
- Stability
- Security

---

## Jenkins Controller (Master)

### Responsibilities
- Hosts Jenkins UI and REST API
- Stores job and pipeline configurations
- Manages plugins
- Schedules jobs
- Allocates executors
- Maintains build queue
- Coordinates agents

### What the Controller Must NOT Do
- Run heavy builds
- Execute Selenium or UI tests
- Consume high CPU or memory

> A busy controller leads to unstable Jenkins.

---

## Jenkins Agent (Slave / Node)

### Responsibilities
- Executes pipeline stages
- Runs builds and tests
- Hosts required tools (Java, Maven, browsers, Docker)
- Creates and manages workspaces

### Agent Characteristics
- OS-specific (Linux, Windows, macOS)
- Can be static or dynamic
- Can run multiple jobs using executors

---

## Executors Explained

- An **executor** is a slot for running a job
- Configured per agent
- Controls parallel execution

### Example
- 1 Agent with 2 executors
- → 2 builds can run in parallel on that agent

---

## Why Controller Should Stay Lightweight

Reasons:
- Plugin stability
- Faster scheduling
- Reduced failure impact
- Easier recovery

**Best practice:**  
> Always offload execution to agents.

---

## Common Interview Questions

- **Where is the workspace created?**  
  → On the agent

- **Can Jenkins run without agents?**  
  → Yes, but not recommended for production

- **What happens if an agent goes offline?**  
  → Job waits or fails based on configuration

- **Can one agent run multiple jobs?**  
  → Yes, controlled by executors

---

## Production Best Practices

- One controller, multiple agents
- Minimal plugins on controller
- Dedicated agents for heavy workloads
- Isolate agents by purpose using labels