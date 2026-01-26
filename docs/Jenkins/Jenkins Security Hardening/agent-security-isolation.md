---
sidebar_position: 5
---

# Agent Security & Isolation

Jenkins agents execute **untrusted and user-controlled code**.
If agents are not isolated properly, they become the easiest entry point for attackers.

---

## Why Agent Security Matters

Agent compromise can lead to:
- Credential theft
- Lateral movement to other systems
- Controller compromise
- Infrastructure abuse

Assume **every build is potentially hostile**.

---

## Trust Model: Controller vs Agents

- Controller: trusted, sensitive, minimal execution
- Agents: untrusted, disposable, isolated

Never treat agents as trusted machines.

---

## Isolation Strategies

### Static Agents (Least Secure)
- Long-lived
- Shared state
- High blast radius

Use only for trusted workloads.

---

### Docker Agents
- Container-level isolation
- Shared host kernel
- Moderate security

Good baseline isolation.

---

### Kubernetes Agents (Recommended)
- Pod-level isolation
- Namespace separation
- Resource limits

Best balance of security and scalability.

---

## One Build per Agent Rule

Strongly recommended:
- One executor per agent
- One pipeline per agent

This prevents:
- Cross-build contamination
- Secret leakage
- State bleed

---

## Credential Exposure Control

Rules:
- Never store secrets on agent filesystem
- Use short-lived credentials
- Scope credentials per job
- Avoid global credentials

Prefer runtime injection.

---

## Network Isolation

- Separate agent networks
- Restrict outbound traffic
- Block access to controller APIs where possible

Agents should not talk freely.

---

## Agent Permissions

- No root access
- No cloud admin permissions
- Minimal IAM roles
- No SSH access between agents

---

## Kubernetes-Specific Hardening

- Use dedicated namespaces
- Enable Pod Security Standards
- Avoid privileged containers
- Disable hostPath volumes

---

## Common Agent Security Failures

- Reusing static agents
- Running multiple builds per agent
- Over-privileged cloud IAM roles
- Agents with SSH access to controller

---

## Best Practices

- Ephemeral agents only
- One build per agent
- Tight network rules
- Separate prod and non-prod agents
- Regularly rotate credentials

---

## Interview Focus Areas

- Why agents are untrusted
- Static vs ephemeral agent risk
- Isolation strategies
- Kubernetes vs Docker agent security

