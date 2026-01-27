---
sidebar_position: 8
---

# Terraform Best Practices & Security

This chapter focuses on **how teams safely operate Terraform in production**.
Most Terraform incidents are not caused by missing features, but by **poor practices and weak safeguards**.

This phase ties together **everything you learned so far**.

---

## Why Best Practices Matter So Much in Terraform

Terraform has the power to:
- Create entire environments in minutes
- Destroy production infrastructure just as fast

Because Terraform is **state-driven**, mistakes can propagate quickly.

Best practices exist to:
- Reduce blast radius
- Prevent human error
- Protect sensitive data
- Enforce consistency

---

## Repository Design & Folder Structure

A clean repository structure improves:
- Readability
- Safety
- Team collaboration

### Recommended Enterprise Structure

```
terraform/
├── modules/
│   ├── networking/
│   ├── security/
│   ├── compute/
│   └── database/
└── env/
    ├── dev/
    ├── stage/
    └── prod/
```

### Why This Works
- Modules are reusable
- Environments are isolated
- State is separated per environment

Avoid mixing environments in the same directory.

---

## Naming Conventions (Why They Matter)

Naming is not cosmetic.

Good naming:
- Reduces confusion
- Improves troubleshooting
- Helps during incidents

### Best Practices
- Use lowercase
- Use consistent separators
- Include environment identifiers
- Avoid abbreviations

Example:
```
app-prod-alb
app-stage-rds
```

---

## Secrets Management (CRITICAL AREA)

Terraform must **never be a secret store**.

### Common Anti-Patterns
❌ Hardcoding secrets  
❌ Storing secrets in tfvars  
❌ Outputting secrets  
❌ Committing state files  

### Correct Approach
Terraform should:
- Reference secrets
- Fetch them at runtime
- Never store them permanently

---

## Secure Secret Sources

Recommended tools:
- AWS Secrets Manager
- AWS SSM Parameter Store
- HashiCorp Vault
- CI/CD injected secrets

Terraform reads secrets, but does not own them.

---

## Terraform State Security (Often Overlooked)

Terraform state may contain:
- Passwords
- Tokens
- IP addresses
- Resource relationships

### State Protection Rules
- Use remote state
- Enable encryption
- Enable versioning
- Restrict IAM access

Treat state like **production credentials**.

---

## IAM Permissions for Terraform

Terraform IAM roles should:
- Be environment-specific
- Use least privilege
- Separate read and write access

Example:
- Plan role (read-only)
- Apply role (write)

Never use admin access casually.

---

## Formatting & Validation (Baseline Safety)

### terraform fmt
```bash
terraform fmt
```
Enforces consistent formatting.

### terraform validate
```bash
terraform validate
```
Catches syntax and logical errors early.

Run both locally and in CI.

---

## Static Analysis & Policy Enforcement

### TFLint
- Detects provider-specific issues
- Enforces best practices

### Checkov
- Security & compliance scanning
- Policy-based enforcement

These tools catch mistakes **before apply**.

---

## Version Control & Change Discipline

Terraform must follow **GitOps principles**.

Rules:
- One change per PR
- Mandatory review
- No direct prod applies
- CI-generated plans only

Humans review. Machines apply.

---

## Preventing Accidental Destruction

Terraform provides safety tools.

```hcl
lifecycle {
  prevent_destroy = true
}
```

Additional safeguards:
- Manual approvals
- Separate prod pipelines
- Restricted IAM roles

Production destruction should be **hard**.

---

## Environment Isolation (Non-Negotiable)

Each environment must have:
- Separate state backend
- Separate credentials
- Separate CI/CD pipeline

Never share:
❌ State  
❌ Credentials  
❌ Pipelines  

---

## Lessons from Real Incidents

Common outage causes:
- Wrong environment applied
- Shared state across envs
- Missing lifecycle protection
- Unreviewed changes

Terraform does exactly what you tell it.

---

## Interview Perspective

Expect questions like:
- How do you secure Terraform state?
- How do you manage secrets?
- How do teams prevent mistakes?
- How do you structure repos?

---

## Final Checklist (Production Readiness)

✅ Remote state with locking  
✅ Version pinning  
✅ Modular design  
✅ Secrets externalized  
✅ CI/CD enforced  
✅ Manual approvals  

---

## Summary

You now understand:
- How to operate Terraform safely
- How teams structure repositories
- How secrets and state are protected
- How incidents are prevented
- How production discipline is enforced

These practices are what turn Terraform into a **reliable production tool**.

---

➡️ Next: Terraform CI/CD & Automation (Complete & Deep)
