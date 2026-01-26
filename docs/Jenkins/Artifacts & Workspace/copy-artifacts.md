---
sidebar_position: 5
---

# Copy Artifacts

The **Copy Artifacts** mechanism allows Jenkins to **reuse build outputs across jobs**.
It is commonly used in **upstream/downstream pipelines**.

---

## What Is Copy Artifacts?

Copy Artifacts enables a job to:
- Fetch artifacts from another job
- Use outputs produced by upstream builds
- Decouple build and deploy pipelines

This is different from `stash`, which works only within a single pipeline.

---

## When to Use Copy Artifacts

Use Copy Artifacts when:
- Build and deploy are separate jobs
- Multiple jobs consume the same artifact
- You want clear upstream/downstream separation

Typical example:
- Job A → Build
- Job B → Deploy using artifacts from Job A

---

## Plugin Requirement

- Requires **Copy Artifact Plugin**
- Must be installed on the controller

---

## Basic Usage (Freestyle Job)

```text
Build → Copy artifacts from another project
```

You configure:
- Source project
- Build selector (last successful, specific build)
- Target directory

---

## Usage in Pipelines

```groovy
copyArtifacts(
  projectName: 'build-job',
  selector: lastSuccessful(),
  filter: 'target/*.jar'
)
```

---

## Build Selectors

Common selectors:
- `lastSuccessful()`
- `lastCompleted()`
- `specific('123')`
- `upstream()`

Selectors determine **which build’s artifacts** are copied.

---

## Permissions & Security

- Source job must allow artifact access
- Use role-based access control
- Avoid copying sensitive artifacts broadly

---

## Copy Artifacts vs archiveArtifacts

| Feature | Copy Artifacts | archiveArtifacts |
|------|----------------|------------------|
| Purpose | Reuse artifacts | Persist artifacts |
| Cross-job | ✅ | ❌ |
| Requires plugin | ✅ | ❌ |
| Storage | Controller | Controller |

---

## Common Mistakes

- Using copyArtifacts instead of stash
- No access permissions
- Copying large artifacts unnecessarily
- Tight coupling between jobs

---

## Best Practices

- Keep build and deploy jobs separate
- Use fingerprints for traceability
- Clean copied artifacts after use
- Document upstream/downstream relationships

---

## Interview Traps

- **Can stash share artifacts across jobs?**  
  → No

- **Does copyArtifacts persist files?**  
  → No, it copies existing ones

- **Is copyArtifacts pipeline-only?**  
  → No, works with freestyle too
