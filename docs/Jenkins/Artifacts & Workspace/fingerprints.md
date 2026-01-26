---
sidebar_position: 4
---

# Fingerprints

Fingerprints allow Jenkins to **track which build produced or used an artifact**.
They are useful for **traceability and auditing**, especially in regulated environments.

---

## What Are Fingerprints?

A fingerprint is a **hash (checksum)** of a file that Jenkins records.
It helps answer questions like:
- Which build produced this artifact?
- Which downstream jobs used it?
- Where did this binary come from?

---

## Why Fingerprints Matter

Fingerprints are useful for:
- Artifact traceability
- Dependency tracking
- Audits and compliance
- Debugging production issues

> Not every pipeline needs fingerprints, but some absolutely do.

---

## How Fingerprinting Works

1. Jenkins calculates a hash of the file
2. Stores the fingerprint metadata
3. Links the file to the build
4. Tracks downstream usage

---

## Enabling Fingerprints

### With `archiveArtifacts`

```groovy
archiveArtifacts artifacts: 'target/app.jar', fingerprint: true
```

This fingerprints the archived artifact.

---

### Fingerprinting Without Archiving

```groovy
fingerprint 'target/app.jar'
```

Use this when you want tracking without retention.

---

## Where Fingerprints Are Stored

- Stored in Jenkins metadata
- Associated with build records
- Visible in Jenkins UI

---

## Typical Use Cases

- Tracking binaries across environments
- Verifying which build was deployed
- Compliance and audit trails

---

## Performance Considerations

- Fingerprinting adds overhead
- Avoid fingerprinting large files unnecessarily
- Use selectively

---

## Common Mistakes

- Fingerprinting everything blindly
- Assuming fingerprints store the file
- Using fingerprints as artifact storage

---

## Best Practices

- Fingerprint only critical artifacts
- Combine with archiveArtifacts when needed
- Document fingerprint usage
- Clean up old builds

---

## Interview Traps

- **Do fingerprints store the file?**  
  → No

- **What do fingerprints track?**  
  → File lineage

- **Are fingerprints mandatory?**  
  → No
