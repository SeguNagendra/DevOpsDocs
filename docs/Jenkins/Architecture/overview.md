---
sidebar_position: 1
---

# Jenkins Architecture – Overview

This section introduces the **core architectural concepts of Jenkins**.  
Understanding this is mandatory before learning pipelines, shared libraries, or cloud setups.

---

## What Is Jenkins Architecture?

Jenkins follows a **distributed, controller-driven architecture** designed to:

- Scale builds horizontally
- Isolate workloads
- Support multiple platforms (Linux, Windows, macOS)
- Handle parallel and concurrent executions safely

At a high level, Jenkins is composed of:
- A **Controller** (formerly Master)
- One or more **Agents** (formerly Slaves)

---

## Terminology (Important)

| Legacy Term | Current Term |
|------------|--------------|
| Master     | Controller   |
| Slave      | Agent / Node |

> Both terms are still used in interviews and real projects. You must know both.

---

## Why Distributed Architecture?

Running everything on a single machine leads to:

- Performance bottlenecks
- Resource exhaustion
- Unstable Jenkins instances

Distributed architecture solves this by:
- Keeping the controller lightweight
- Offloading execution to agents
- Allowing parallelism and scalability

---

## Core Architectural Components

You will study each of these in detail in this section:

- Controller
- Agent (Node)
- Executors
- Workspace
- Queue
- Distributed build execution flow

Each component has **a dedicated document** in this folder.
