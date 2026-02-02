---
sidebar_position: 16
---

# Advanced Branch & PR Strategies – Handling Real Repositories

As teams grow and repositories become more complex, branch strategy plays a huge role
in how effective SonarQube analysis is.

This chapter explains **advanced branch and pull request strategies** that work well in real-world projects.

---

## Why Branch Strategy Matters for SonarQube

SonarQube evaluates code **by comparison**:
- New code vs existing code
- Feature branch vs target branch

A poor branching strategy can:
- Produce confusing results
- Hide real issues
- Create unnecessary noise

A clear strategy keeps analysis meaningful.

---

## Long-Lived vs Short-Lived Branches

### Long-Lived Branches
Examples:
- main
- master
- develop

Used for:
- Tracking overall code health
- Monitoring trends over time

SonarQube maintains history for these branches.

---

### Short-Lived Branches
Examples:
- feature branches
- bugfix branches

Used for:
- Pull requests
- Focused analysis on changes only

SonarQube analyzes only new code for these branches.

---

## Pull Request Analysis Strategy

Best practice for PRs:
- Run analysis on every PR
- Compare against the target branch
- Apply Quality Gates to new code only

This prevents new problems without blocking legacy cleanup.

---

## Baseline and New Code Definition

SonarQube determines new code based on:
- Previous version
- Reference branch
- Specific date (optional)

Choosing the right baseline:
- Prevents false failures
- Keeps gates fair
- Supports gradual improvement

---

## Handling Legacy Codebases

For large legacy projects:
- Do not try to fix everything at once
- Establish a clean baseline
- Enforce strict rules only on new code

This approach encourages progress without frustration.

---

## Monorepo Considerations

In monorepos:
- Multiple projects share one repository
- Different teams own different modules

Best practices:
- Define clear project boundaries
- Avoid scanning unrelated code
- Assign ownership correctly

SonarQube can handle monorepos well when configured properly.

---

## Common Branch Strategy Mistakes

Avoid these patterns:
- Treating all branches the same
- Running full analysis on every feature branch
- Ignoring baseline configuration
- Mixing experimental and production code

These mistakes reduce trust in results.

---

## Key Takeaway

Advanced branch strategies make SonarQube:
- Fair
- Predictable
- Scalable

Good branch design ensures SonarQube supports development instead of slowing it down.

---

➡️ **Next:** Custom Rules & Plugins  
