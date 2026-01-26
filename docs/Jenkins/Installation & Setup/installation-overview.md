---
sidebar_position: 1
---

# Jenkins Installation – Overview

This section covers **how Jenkins is installed and bootstrapped** for real-world usage.
Installation choices directly affect **stability, scalability, and maintenance**.

---

## Why Installation Matters

A poorly installed Jenkins leads to:
- Plugin instability
- Upgrade failures
- Performance issues
- Difficult recovery

A clean installation ensures:
- Predictable upgrades
- Easier backups
- Better security

---

## Supported Installation Approaches

Jenkins can be installed in multiple ways. Each has its place.

### 1. Local Installation
- Installed directly on VM or machine
- Suitable for:
  - Learning
  - Small teams
  - PoC environments

### 2. Docker-Based Installation
- Jenkins runs inside a container
- Suitable for:
  - Consistent environments
  - Easy upgrades
  - Modern CI/CD setups

---

## What This Section Covers

You will learn:
- Local Jenkins installation (Linux / macOS / Windows)
- Docker-based Jenkins installation
- Initial admin setup
- Plugin installation strategy
- Tool configuration basics

Each topic is documented **in a separate file**.

---

## Installation Prerequisites

Before installing Jenkins:
- Java (LTS version)
- Adequate disk space
- Network access for plugins
- SCM access (Git)

---

## Recommended Installation Choice

| Environment | Recommendation |
|-----------|----------------|
| Learning | Local install |
| Team CI | Docker |
| Enterprise | Docker + agents |
| Cloud | Docker / Kubernetes |
