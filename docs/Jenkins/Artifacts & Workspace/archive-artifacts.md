---
sidebar_position: 2
---

# archiveArtifacts

The `archiveArtifacts` step is used to **persist build outputs after a pipeline finishes**.
It is one of the most important steps for reporting, debugging, and auditing.

---

## What Does `archiveArtifacts` Do?

`archiveArtifacts`:
- Copies files from the workspace
- Stores them with the build record
- Makes them available after build completion

Artifacts are stored on the **controller**, not the agent.

---

## Basic Usage

```groovy
post {
  always {
    archiveArtifacts artifacts: '**/target/*.jar'
  }
}
```

This archives all JAR files under `target` directories.

---

## Where Artifacts Live

- Artifacts are attached to a specific build
- Accessible via Jenkins UI
- Downloadable anytime (based on retention)

---

## Wildcards & Patterns

Common patterns:
- `**/*.log`
- `**/reports/**`
- `target/*.jar`

Use precise patterns to avoid large uploads.

---

## Allow Empty Archives

```groovy
archiveArtifacts artifacts: 'reports/**', allowEmptyArchive: true
```

Useful when:
- Reports are generated conditionally
- You don’t want pipeline failure

---

## Retention & Cleanup

Artifacts are affected by:
- Build discarder settings
- Disk usage limits

> Always configure log rotation.

---

## archiveArtifacts vs stash

| Feature | archiveArtifacts | stash |
|------|------------------|------|
| Purpose | Persist results | Share data |
| Scope | Across builds | Within pipeline |
| Stored on | Controller | Controller |
| Retained | Yes | No (temporary) |

---

## Common Mistakes

- Archiving entire workspace
- No build discarder configured
- Confusing stash with archive
- Archiving secrets accidentally

---

## Best Practices

- Archive only what you need
- Use post block
- Keep artifact size small
- Combine with buildDiscarder

---

## Interview Traps

- **Where are artifacts stored?**  
  → Controller

- **Do artifacts persist after build?**  
  → Yes

- **Can artifacts be used across jobs?**  
  → Yes (via Copy Artifacts)