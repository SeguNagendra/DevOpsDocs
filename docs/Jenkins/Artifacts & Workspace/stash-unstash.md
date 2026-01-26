---
sidebar_position: 3
---

# stash & unstash

`stash` and `unstash` are used to **share files between stages within the same pipeline**.
They are often misunderstood and misused in real projects.

---

## What Are `stash` and `unstash`?

- `stash` temporarily stores files from a workspace
- `unstash` restores those files into another workspace

They are designed for **intra-pipeline data transfer**, not persistence.

---

## When to Use stash / unstash

Use them when:
- Different stages run on different agents
- You need build output in later stages
- Workspace is not shared across agents

Common example:
- Build on Linux agent
- Test on another agent
- Deploy on a Docker agent

---

## Basic Usage

### Stash Files

```groovy
stash name: 'build-output', includes: 'target/*.jar'
```

### Unstash Files

```groovy
unstash 'build-output'
```

---

## Typical Pipeline Example

```groovy
stage('Build') {
  steps {
    sh 'mvn package'
    stash name: 'jar', includes: 'target/*.jar'
  }
}

stage('Deploy') {
  steps {
    unstash 'jar'
    sh 'deploy.sh'
  }
}
```

---

## Scope & Lifecycle

| Aspect | stash / unstash |
|------|-----------------|
| Scope | Same pipeline only |
| Retention | Temporary |
| Persist after build | ❌ |
| Use across jobs | ❌ |

> Stashed data is deleted after the pipeline completes.

---

## stash vs archiveArtifacts

| Feature | stash | archiveArtifacts |
|------|------|------------------|
| Purpose | Share data | Persist data |
| Lifetime | Temporary | Long-term |
| Cross-job | ❌ | ✅ |
| Storage | Controller | Controller |

---

## Performance Considerations

- Stash uploads data to controller
- Large stashes slow pipelines
- Avoid stashing big directories

---

## Common Mistakes

- Using stash as artifact storage
- Stashing entire workspace
- Forgetting unstash
- Name collisions

---

## Best Practices

- Stash only required files
- Use clear stash names
- Clean workspace before unstash if needed
- Prefer archiveArtifacts for reports

---

## Interview Traps

- **Does stash persist after build?**  
  → No

- **Can stash be shared across jobs?**  
  → No

- **Where is stash stored?**  
  → Controller (temporarily)
