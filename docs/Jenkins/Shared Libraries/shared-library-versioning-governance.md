---
sidebar_position: 5
---

# Shared Library Versioning & Governance

Shared libraries are **production code**.
Without versioning and governance, they become a single point of failure across all pipelines.

---

## Why Versioning Matters

If all pipelines use the same library version:
- A bad change breaks every pipeline
- Rollbacks are hard
- Debugging becomes slow

Versioning allows:
- Safe upgrades
- Controlled rollouts
- Easy rollback

---

## Versioning Strategies

### Branch-Based Versioning

```groovy
@Library('ci-lib@main') _
```

Pros:
- Simple
- Fast iteration

Cons:
- Risky for production

---

### Tag-Based Versioning (Recommended)

```groovy
@Library('ci-lib@v1.2.0') _
```

Pros:
- Immutable
- Predictable
- Easy rollback

Cons:
- Requires release discipline

---

### Commit Hash Pinning

```groovy
@Library('ci-lib@a1b2c3d') _
```

Pros:
- Absolute reproducibility

Cons:
- Hard to manage at scale

---

## Upgrade Strategy

Recommended approach:
1. Develop on `main`
2. Test in non-prod pipelines
3. Tag a release
4. Upgrade prod pipelines explicitly

Never auto-upgrade production pipelines.

---

## Governance Model

Define:
- Owners of shared library
- Code review requirements
- Release approval process

Shared libraries should have **stricter rules** than app repos.

---

## Access Control

- Limit who can modify shared libs
- Restrict Jenkins admin access
- Use protected branches
- Enforce PR reviews

---

## Backward Compatibility

Breaking changes should:
- Be versioned clearly
- Be documented
- Not be silently introduced

Prefer additive changes.

---

## Testing Shared Libraries

- Unit test Groovy logic (outside Jenkins)
- Test changes in sandbox Jenkins
- Avoid testing directly in production

---

## Common Failures

- Using `main` everywhere
- No release tags
- Silent breaking changes
- Too many owners

---

## Best Practices

- Tag releases
- Pin versions in pipelines
- Maintain changelog
- Assign clear ownership
- Treat shared libs as products

---

## Interview Focus Areas

- Why pin shared library versions
- Branch vs tag usage
- Governance importance

