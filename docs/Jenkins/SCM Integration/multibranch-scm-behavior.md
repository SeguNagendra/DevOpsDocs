---
sidebar_position: 4
---

# Multibranch SCM Behavior

This document explains **how Jenkins Multibranch Pipelines interact with SCM systems**.
Understanding this behavior is critical to avoid missed builds, duplicate jobs, and unexpected executions.

---

## What Is Multibranch SCM Behavior?

In a multibranch pipeline, Jenkins does **not** build a single branch.
Instead, it:

- Scans the repository
- Discovers branches and pull requests
- Creates jobs dynamically per branch
- Executes the Jenkinsfile from each branch

---

## Branch Indexing

### What Is Branch Indexing?

Branch indexing is the process where Jenkins:
- Queries the SCM
- Detects new, updated, or deleted branches
- Syncs Jenkins jobs with SCM state

---

### When Branch Indexing Happens

Branch indexing is triggered by:
- Webhook events (preferred)
- Periodic scan schedule
- Manual scan

> Webhooks trigger indexing, not direct builds.

---

## Jenkinsfile Discovery Rules

For a branch to be built:
- A `Jenkinsfile` must exist in the branch
- The Jenkinsfile path must match configuration

If missing:
- Branch is ignored
- No job is created

---

## Pull Request Behavior

For PRs, Jenkins:
- Creates a virtual branch (SCM-specific)
- Runs the Jenkinsfile
- Associates build with PR

This enables:
- PR validation
- Status checks
- Early failure detection

---

## Branch Deletion Handling

When a branch is deleted in SCM:
- Jenkins marks the job as orphaned
- Orphaned jobs can be:
  - Disabled
  - Deleted automatically (recommended)

---

## Build Triggers in Multibranch

- Builds are triggered by indexing results
- Not all indexing results in builds
- Changes in Jenkinsfile can retrigger pipelines

---

## Common Misunderstandings

- Webhooks trigger builds directly ❌
- Every branch always builds ❌
- Jenkinsfile is optional ❌

---

## Performance Considerations

- Large repos → expensive scans
- Too frequent indexing → controller load
- Use webhook-based indexing

---

## Best Practices

- Enable webhook-based indexing
- Configure orphaned item cleanup
- Keep Jenkinsfile lightweight
- Use branch-based conditions inside pipeline

---

## Interview Focus Areas

- Difference between indexing and build
- How PR builds work internally
- Why Jenkinsfile location matters

