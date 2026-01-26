---
sidebar_position: 4
---

# Multibranch Pipeline

Multibranch Pipeline is the **standard job type for team-based development**.
It automatically manages pipelines for all branches and pull requests.

---

## What Is a Multibranch Pipeline?

A Multibranch Pipeline:
- Scans a source control repository
- Detects branches and pull requests
- Automatically creates a pipeline for each branch
- Executes Jenkinsfile per branch

> This removes the need to create jobs manually.

---

## Why Multibranch Pipelines Are Important

Without multibranch pipelines:
- Teams create separate jobs per branch
- Configuration drift occurs
- PR validation becomes manual

With multibranch pipelines:
- CI is automatic
- Branches are isolated
- PRs are validated consistently

---

## How Multibranch Pipelines Work

1. Jenkins scans SCM repository
2. Finds branches and PRs
3. Looks for a Jenkinsfile
4. Creates jobs dynamically
5. Executes pipeline per branch

---

## Jenkinsfile Requirement

Each branch must contain:
```
Jenkinsfile
```

Branch-specific logic can be added using conditions.

---

## Typical Use Cases

- Feature branch validation
- Pull request builds
- Main / develop branch pipelines
- Team-based CI workflows

---

## Branch-Based Conditions

```groovy
when {
  branch 'main'
}
```

Used for:
- Deployments
- Environment-specific steps

---

## Multibranch vs Pipeline Job

| Feature | Pipeline Job | Multibranch Pipeline |
|-------|--------------|---------------------|
| Single branch | ✅ | ❌ |
| Multiple branches | ❌ | ✅ |
| PR builds | ❌ | ✅ |
| Auto discovery | ❌ | ✅ |

---

## Common Mistakes

- Missing Jenkinsfile in repo
- Heavy logic inside branch conditions
- Not cleaning orphaned branches

---

## Production Best Practices

- Use multibranch for all team repos
- Enable periodic branch indexing
- Clean up old branches automatically
- Keep Jenkinsfile simple

---

## Interview Perspective

- Multibranch pipelines are expected knowledge
- Explain branch discovery clearly
- Highlight PR validation
