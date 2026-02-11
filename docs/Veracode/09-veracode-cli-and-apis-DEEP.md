---
sidebar_position: 9
title: Veracode CLI and APIs
---

# Veracode CLI and APIs
**Automation & Scale for DevOps Engineers**

This module explains how **DevOps engineers automate Veracode at scale** using the **Veracode CLI and REST APIs**.

If CI/CD integration answers *how to plug Veracode into pipelines*,  
this module answers:
> **How do I make Veracode fully automated, repeatable, and scalable across many apps and teams?**

---

## 1. Why CLI & APIs Matter in DevOps

UI-driven security does not scale.

Problems with UI-only usage:
- Manual uploads
- Inconsistent behavior
- Hard to audit
- Impossible to standardize across repos

CLI and APIs allow:
- Scripted automation
- Pipeline standardization
- Large-scale adoption
- Zero manual steps

For DevOps, **automation is non-negotiable**.

---

## 2. Veracode CLI – What It Is

The **Veracode CLI** is a command-line tool that allows you to:
- Authenticate securely
- Upload artifacts
- Trigger scans
- Check scan status
- Fetch results programmatically

The CLI is designed for:
- CI/CD pipelines
- Automation scripts
- Headless environments

---

## 3. Authentication Models (Critical for Security)

### Service Accounts (Recommended)
- Dedicated accounts for CI/CD
- No human login dependency
- Limited permissions

### Authentication Methods
- API credentials
- Token-based authentication

### DevOps Best Practices
- Never use personal accounts
- Store secrets in CI secret managers
- Rotate credentials
- Apply least privilege

Most security incidents start with poor secret handling.

---

## 4. Using CLI in CI/CD Pipelines (Conceptual Flow)

Typical flow:
1. CI builds artifact
2. CLI uploads artifact
3. Scan is triggered
4. Pipeline polls scan status
5. Policy result is checked
6. Pipeline proceeds or fails

Everything happens **without UI interaction**.

---

## 5. Asynchronous Automation (Best Practice)

### Why Asynchronous Is Better
- Avoid long pipeline blocking
- Better CI performance
- Scales to large applications

### Typical Pattern
- Trigger scan
- Store scan ID
- Poll periodically
- Act on final result

Asynchronous patterns are essential for **enterprise pipelines**.

---

## 6. Veracode REST APIs – Overview

Veracode provides APIs to:
- Manage applications
- Trigger scans
- Fetch findings
- Retrieve reports
- Integrate with dashboards

APIs allow:
- Custom tooling
- Centralized reporting
- Advanced automation

---

## 7. Common API Use Cases (DevOps-Focused)

### Application Management
- Create applications automatically
- Standardize naming
- Apply metadata consistently

### Reporting
- Pull vulnerability metrics
- Track security debt
- Feed dashboards

### Automation
- Enforce organization-wide standards
- Reduce manual setup
- Enable self-service pipelines

---

## 8. Secrets Management & Security

### Where to Store Secrets
- Jenkins credentials store
- GitHub Actions secrets
- GitLab CI variables
- Vault or cloud secret managers

### What NOT to Do
- Hardcode secrets
- Print secrets to logs
- Share credentials across teams

Secrets handling is part of **DevOps security responsibility**.

---

## 9. Scaling Veracode with Automation

Challenges at scale:
- Hundreds of repos
- Multiple languages
- Different teams

Solutions:
- Shared pipeline templates
- Centralized CLI scripts
- API-driven onboarding
- Consistent policies

Automation turns Veracode from a tool into a **platform**.

---

## 10. Error Handling & Reliability

Automation must handle failures gracefully.

Common failures:
- Network issues
- Authentication errors
- Scan timeouts

DevOps best practices:
- Retry transient failures
- Fail fast on policy violations
- Log clearly
- Alert appropriately

---

## 11. Common DevOps Mistakes with CLI & APIs

Avoid these:
- Manual uploads mixed with automation
- Long-running blocking jobs
- Hardcoded credentials
- One script for all apps
- No error handling

These mistakes destroy trust in security automation.

---

## 12. Key Takeaways

- CLI & APIs enable full automation
- UI does not scale
- Service accounts are mandatory
- Async automation works best
- APIs unlock enterprise usage
- DevOps owns reliability and scale

---

## What’s Next?

Next module covers:
- Results analysis & remediation
- How DevOps helps developers fix issues
- Managing security debt
