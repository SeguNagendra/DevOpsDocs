---
sidebar_position: 6
---

# Ephemeral & Cloud Agents

Ephemeral agents are **short-lived, on-demand agents** created dynamically for builds.
They are key to **elastic scaling and cost optimization** in Jenkins.

---

## What Is an Ephemeral Agent?

An ephemeral agent:
- Is created when a build starts
- Runs one (or few) builds
- Is destroyed after completion

This avoids idle infrastructure.

---

## Common Ephemeral Agent Platforms

- Cloud VMs (AWS EC2, Azure VM, GCP Compute)
- Kubernetes pods
- Container-based cloud runners

All follow the same lifecycle principle.

---

## Why Use Ephemeral Agents

Ephemeral agents help when:
- Build traffic is bursty
- Cost optimization matters
- Isolation is required
- Multiple teams share Jenkins

---

## Cloud VM–Based Ephemeral Agents

Typical flow:
1. Jenkins requests a VM
2. Cloud plugin provisions VM
3. Agent connects to controller
4. Build runs
5. VM is terminated

Often used with:
- Auto Scaling Groups
- Spot / preemptible instances

---

## Kubernetes vs Cloud VM Agents

| Aspect | Cloud VM Agents | Kubernetes Agents |
|------|-----------------|-------------------|
| Provision speed | Slower | Faster |
| Cost efficiency | Medium | High |
| Infra complexity | Higher | Lower |
| Scaling granularity | VM-level | Pod-level |
| Preferred today | Less | More |

---

## Agent Templates

Templates define:
- OS / image
- Tools
- Labels
- Executors
- Resource limits

Templates ensure consistency.

---

## Cost Control Techniques

- One build per agent
- Spot / preemptible instances
- Aggressive idle timeout
- Small base images

---

## Common Mistakes

- Long-lived cloud agents
- Too many executors per agent
- No termination timeout
- Mixing prod and non-prod workloads

---

## Best Practices

- Prefer ephemeral over static agents
- One executor per ephemeral agent
- Use labels for isolation
- Monitor agent creation failures

---

## Security Considerations

- Agents run untrusted code
- Use minimal permissions
- Rotate credentials
- Isolate networks

---

## Interview Focus Areas

- Ephemeral vs static agents
- Cloud VM vs Kubernetes agents
- Cost optimization strategies

