---
sidebar_position: 4
---

# Shared vs Dedicated Controllers

One of the most important enterprise decisions is whether teams should **share Jenkins controllers**
or use **dedicated controllers**. This decision affects cost, stability, security, and velocity.

---

## The Core Trade-Off

- **Shared controllers** → lower cost, higher coupling
- **Dedicated controllers** → higher cost, stronger isolation

There is no universal answer; context matters.

---

## Shared Controllers

### Characteristics
- Multiple teams on one controller
- Folder-based RBAC
- Shared plugin catalog
- Shared controller resources

### Advantages
- Lower infrastructure cost
- Easier central management
- Faster onboarding

### Risks
- Plugin conflicts
- Performance contention
- Larger blast radius
- Slower upgrades

---

## Dedicated Controllers

### Characteristics
- One team or domain per controller
- Independent plugins and upgrades
- Dedicated agent pools
- Clear ownership

### Advantages
- Strong isolation
- Independent release cycles
- Reduced blast radius
- Easier compliance

### Trade-Offs
- Higher operational overhead
- Increased cost
- More controllers to manage

---

## Hybrid Model (Most Enterprises)

Common pattern:
- Shared controllers for non-prod
- Dedicated controllers for prod or regulated teams
- Specialized controllers for special workloads

Hybrid balances cost and risk.

---

## Decision Factors

Consider:
- Regulatory requirements
- Team maturity
- Plugin diversity
- Build volume
- Risk tolerance

Architecture must match reality.

---

## Migration Strategy

Typical progression:
1. Start with shared controller
2. Introduce folder isolation
3. Split high-risk teams
4. Move critical workloads to dedicated controllers

Avoid big-bang migrations.

---

## Cost Optimization Techniques

- Right-size controllers
- Consolidate low-usage controllers
- Share agent infrastructure safely
- Automate controller provisioning

Cost control matters at scale.

---

## Common Mistakes

- Forcing all teams onto one controller
- Spinning controllers per team prematurely
- Ignoring plugin conflicts
- No ownership model

---

## Best Practices

- Default to shared, isolate when needed
- Use hybrid model consciously
- Revisit decisions periodically
- Automate controller lifecycle

---

## Interview Focus Areas

- Shared vs dedicated controller trade-offs
- When to split controllers
- Hybrid controller models

