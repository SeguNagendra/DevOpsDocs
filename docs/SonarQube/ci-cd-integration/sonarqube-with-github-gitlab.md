---
sidebar_position: 13
---

# SonarQube with GitHub / GitLab – Pull Requests & Branch Analysis

Modern development workflows are built around **Git platforms** like GitHub and GitLab.
SonarQube integrates deeply with these platforms to give developers **early, contextual feedback**
directly inside pull requests.

This chapter explains how that integration works and why it is so effective.

---

## Why PR-Based Analysis Matters

In modern teams:
- Code is reviewed through pull requests
- Feedback is expected quickly
- Developers prefer feedback close to their code

PR-based SonarQube analysis:
- Focuses only on changed code
- Avoids overwhelming developers
- Prevents new issues from entering the codebase

This makes quality feedback **actionable**, not noisy.

---

## Branch Analysis vs Pull Request Analysis

SonarQube supports both, and they serve different purposes.

### Branch Analysis
- Runs on long-lived branches (main, develop)
- Tracks overall code health
- Useful for trend analysis

### Pull Request Analysis
- Runs on feature branches or PRs
- Compares changes against target branch
- Focuses on *new code only*

Most teams use PR analysis for day-to-day development.

---

## How PR Decoration Works

PR decoration means:
- SonarQube posts results directly in the PR
- Issues are shown inline or as comments
- Quality Gate status is visible in the PR

This tight feedback loop:
- Speeds up reviews
- Improves learning
- Reduces back-and-forth

---

## Supported Git Platforms

SonarQube supports:
- GitHub
- GitHub Enterprise
- GitLab
- GitLab Enterprise

Configuration differs slightly, but the concepts remain the same.

---

## Authentication & Permissions

Integration usually requires:
- OAuth apps or tokens
- Webhooks between SonarQube and Git platform
- Proper repository permissions

Misconfigured permissions are the most common cause of missing PR decoration.

---

## New Code Comparison Logic

For PRs, SonarQube:
- Compares changes against the target branch
- Applies Quality Gates only to new code
- Ignores pre-existing legacy issues

This keeps feedback fair and focused.

---

## Handling PR Failures

When a PR fails a Quality Gate:
- Developers see exactly what failed
- Fixes can be pushed immediately
- No need to wait for full pipeline completion

This reduces wasted CI time.

---

## Common Integration Mistakes

Avoid these problems:
- Missing webhook configuration
- Using insufficient token permissions
- Scanning PRs like full branches
- Ignoring failed Quality Gates

Most failures are configuration-related.

---

## Best Practices

Follow these guidelines:
- Enable PR decoration for all repos
- Fail PRs on critical issues only
- Educate developers on reading feedback
- Keep rules consistent across teams

Consistency builds trust in the system.

---

## Key Takeaway

Git platform integration brings SonarQube **into the developer workflow**.

When quality feedback appears directly in pull requests:
- Developers respond faster
- Code reviews improve
- Quality becomes a shared responsibility

---

➡️ **Next:** Security & Access Management  
