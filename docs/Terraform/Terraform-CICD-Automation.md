---
sidebar_position: 9
---

# Terraform CI/CD & Automation

In real production environments, **Terraform is never run manually on production systems**.
All changes flow through **automated CI/CD pipelines** with reviews, approvals, and safeguards.

This chapter explains **how teams operationalize Terraform safely**.

---

## Why Terraform Must Run in CI/CD

Running Terraform manually causes:
- Accidental changes in wrong environments
- No audit trail
- Inconsistent executions
- High risk of human error

CI/CD ensures:
- Repeatability
- Reviewability
- Traceability
- Enforcement of best practices

Terraform + CI/CD is **non-negotiable for production**.

---

## Standard Terraform CI/CD Pipeline (Mental Model)

A production-grade pipeline typically follows:

1. Code checkout
2. Terraform init
3. Terraform fmt & validate
4. Terraform plan
5. Manual approval
6. Terraform apply

Each step exists to **reduce risk**.

---

## Terraform Plan as a Contract

The plan output:
- Shows exactly what will change
- Is reviewed by humans
- Is approved before execution

Golden rule:
> **Never apply without reviewing the plan**

In many teams, the plan itself is an approval artifact.

---

## GitHub Actions with Terraform (Deep Dive)

GitHub Actions is widely used for Terraform automation.

### Typical Workflow Pattern
- Pull Request → terraform plan
- Merge to main → terraform apply

### Example (Simplified)
```yaml
name: Terraform Plan

on: [pull_request]

jobs:
  terraform:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: hashicorp/setup-terraform@v2
      - run: terraform init
      - run: terraform validate
      - run: terraform plan
```

Apply should happen only on protected branches.

---

## Jenkins Pipelines for Terraform

In enterprise environments, Jenkins is common.

Typical stages:
- Checkout
- Init
- Validate
- Plan
- Manual approval
- Apply

Key requirement:
- Non-interactive Terraform execution
- Controlled credentials via Jenkins

---

## Environment-Specific Pipelines

Each environment should have:
- Separate pipeline
- Separate credentials
- Separate backend

Example:
- Dev → auto-apply
- Stage → approval required
- Prod → strict approval + limited access

---

## Secrets & Credentials in CI/CD

Terraform should never receive static credentials.

Correct approaches:
- IAM roles assumed by runners
- GitHub Secrets / Jenkins Credentials
- Short-lived credentials

Terraform credentials should:
- Be injected at runtime
- Have minimal permissions
- Be rotated automatically

---

## Remote State in CI/CD

CI/CD pipelines must:
- Use remote state
- Respect state locking
- Fail safely if state is locked

This prevents:
- Concurrent applies
- State corruption

---

## Terraform Cloud & Terraform Enterprise

Terraform Cloud provides:
- Remote execution
- Managed state
- Workspace isolation
- Team access control

Used when:
- Multiple teams share infra
- Compliance is strict
- Central governance is required

---

## Policy as Code (Sentinel – High Level)

Sentinel enforces rules such as:
- No public S3 buckets
- Mandatory tagging
- Approved regions only

Policies block unsafe plans **before apply**.

---

## Approval & Safety Gates

Production pipelines usually include:
- Manual approvals
- Restricted prod roles
- Separate prod accounts

Terraform apply should be **harder** than plan.

---

## Real-World CI/CD Failures

Common issues:
- Wrong credentials used
- Shared pipelines across envs
- Missing approval steps
- Applying outdated plans

Strong pipelines prevent these mistakes.

---

## Interview Perspective

Be ready to explain:
- Terraform pipeline stages
- How approvals work
- Secrets handling strategy
- Terraform Cloud vs OSS

---

## Summary

You now understand:
- Why Terraform belongs in CI/CD
- How pipelines are structured
- How secrets and state are handled
- How approvals protect production
- How teams scale Terraform safely

Terraform automation is about **discipline, not speed**.

---

➡️ Next: Troubleshooting, Interviews & Real-World Scenarios (Complete & Deep)
