---
sidebar_position: 2
---

# Multi-Controller Architecture

At enterprise scale, Jenkins must run **multiple controllers**.
This document explains why, when, and how to design a multi-controller Jenkins architecture.

---

## Why Multiple Controllers Are Required

A single Jenkins controller eventually fails due to:
- Too many jobs and users
- Plugin conflicts across teams
- Security blast radius
- Upgrade coordination problems

Multiple controllers reduce risk and increase scalability.

---

## When to Introduce Multiple Controllers

Strong signals:
- Hundreds of jobs on one controller
- Conflicting plugin requirements
- Different security/compliance needs
- Frequent upgrade outages
- Multiple teams blocking each other

Do not wait for failure to scale out.

---

## Common Multi-Controller Models

### Environment-Based Controllers
- One controller per environment
- Example: dev, test, prod

Useful for strict separation.

---

### Domain or Team-Based Controllers
- One controller per team or domain
- Example: payments, core, analytics

Improves autonomy and velocity.

---

### Hybrid Model (Most Common)
- Shared non-prod controllers
- Dedicated prod controllers
- Special-purpose controllers if needed

Balances cost and isolation.

---

## Controller Responsibilities at Scale

Each controller should:
- Own its job set
- Use its own plugin catalog
- Have independent upgrade cycles
- Isolate credentials and agents

Avoid shared state between controllers.

---

## Shared Components Across Controllers

Safe to share:
- SCM systems
- Artifact repositories
- Shared libraries (with governance)
- Identity providers

Never share `JENKINS_HOME`.

---

## Agent Strategy in Multi-Controller Setups

Options:
- Dedicated agent pools per controller
- Shared Kubernetes clusters with namespaces
- Label-based isolation

Agent isolation is critical.

---

## Upgrade & Failure Isolation

Benefits:
- One controller upgrade does not impact others
- Failures are contained
- Faster rollback and recovery

Isolation improves reliability.

---

## Cost Considerations

Trade-offs:
- More controllers = more infra cost
- But lower blast radius
- Better operational efficiency

Optimize for risk, not minimum cost.

---

## Common Anti-Patterns

- One giant controller
- Sharing plugins across controllers blindly
- Centralizing everything “for simplicity”

These do not scale.

---

## Best Practices

- Start small, scale horizontally
- Standardize controller templates
- Automate provisioning
- Document ownership

---

## Interview Focus Areas

- Why multi-controller Jenkins is needed
- Environment vs team-based controllers
- Hybrid controller models

