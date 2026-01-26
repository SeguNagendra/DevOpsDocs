---
sidebar_position: 5
---

# Branch Filtering & PR Discovery

This document explains **how Jenkins controls which branches and pull requests are built**
in multibranch pipelines. Correct configuration prevents unnecessary builds and reduces load.

---

## Why Branch Filtering Matters

Without filtering:
- Every branch triggers jobs
- Controller load increases
- Noise hides real failures
- Costs increase (agents, time)

Filtering ensures Jenkins builds **only what matters**.

---

## Branch Discovery (High-Level)

Branch discovery controls:
- Which branches Jenkins detects
- Whether to build branches automatically

Typical options:
- Discover all branches
- Discover branches with Jenkinsfile
- Exclude branches by name or pattern

---

## Branch Name Filtering

Use include/exclude patterns to control branches.

Examples:
- Include: `main|develop|release/.*`
- Exclude: `feature/.*|experimental/.*`

Benefits:
- Fewer jobs
- Faster indexing
- Clear CI signal

---

## Pull Request (PR) Discovery

PR discovery allows Jenkins to:
- Detect open PRs
- Run validation pipelines
- Report status back to SCM

Common PR strategies:
- Build PR head only
- Build PR with target branch merge
- Both (costly)

---

## PR Build Strategies (Conceptual)

- **Head only**: Tests PR changes alone
- **Merge with target**: Tests how PR behaves after merge (safer)

Enterprise pipelines usually prefer **merge-based PR builds**.

---

## Forked Repository PRs

Special considerations:
- Limited credentials
- Reduced permissions
- Higher security risk

Best practice:
- Use restricted credentials
- Avoid exposing secrets to forks

---

## Jenkinsfile Path Filtering

Jenkins can be configured to:
- Look for Jenkinsfile in custom paths
- Ignore branches without Jenkinsfile

This reduces accidental builds.

---

## Common Misconfigurations

- Building every branch by default
- No PR validation
- Using merge strategy without understanding cost
- Exposing secrets to forked PRs

---

## Performance Tips

- Filter branches aggressively
- Avoid building archived branches
- Use webhook-triggered indexing
- Limit PR strategies

---

## Interview Focus Areas

- Branch discovery vs filtering
- PR head vs merge strategy
- Security risks with forked PRs

