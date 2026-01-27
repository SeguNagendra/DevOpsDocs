---
sidebar_position: 10
---

# Terraform Troubleshooting & Real-World Scenarios

This final chapter focuses on **what actually breaks in real life**, how to **debug safely**, and how to **think like a senior engineer** during incidents and interviews.

Knowing Terraform commands is not enough.
**Judgment, discipline, and troubleshooting skill** matter most.

---

## How Terraform Fails in the Real World

Terraform rarely fails because of syntax.
It fails because of:
- Process gaps
- Environment mistakes
- State mismanagement
- Human error

Understanding failure modes is critical.

---

## State Lock Issues (Most Common Incident)

### Error
```
Error acquiring the state lock
```

### Why This Happens
- Another apply is running
- Previous run crashed
- CI/CD job was terminated

### Safe Resolution
```bash
terraform force-unlock <LOCK_ID>
```

⚠️ Only unlock when you are **100% sure** no other run is active.

---

## Provider Version Conflicts

### Symptoms
- Code worked yesterday
- Suddenly fails after `init`
- CI and local behave differently

### Root Cause
- Missing provider version pinning
- Module using incompatible provider version

### Fix
- Centralize provider versions
- Re-run:
```bash
terraform init -upgrade
```

---

## Dependency Cycle Errors

### Why They Occur
- Circular references
- Overuse of `depends_on`
- Poor module design

### How to Fix
- Break cycles using data sources
- Refactor modules
- Simplify dependencies

---

## Terraform Plan Analysis (Senior Skill)

Never skim a plan.

Look carefully for:
- Resource replacement (`-/+`)
- Unexpected deletes
- Large blast-radius changes

A good engineer can predict outages by reading plans.

---

## Debugging Terraform Systematically

### Step 1: terraform plan
Always start with plan.

### Step 2: terraform graph
```bash
terraform graph | dot -Tpng > graph.png
```

Use graph to:
- Understand dependency order
- Detect cycles

---

### Step 3: Debug Logs
```bash
TF_LOG=TRACE terraform apply
```

Use logs only for deep provider-level issues.

---

## Infrastructure Drift (Very Common)

### What Is Drift?
Drift happens when:
- Resources are changed manually
- Autoscaling modifies infrastructure
- External systems update config

Terraform detects drift during plan.

### Best Practice
- Treat Terraform as source of truth
- Restrict console access
- Review drift carefully

---

## Safe Refactoring Techniques

Refactoring Terraform without downtime requires discipline.

### Common Tools
- `terraform state mv`
- Lifecycle rules
- Incremental changes

Never delete and recreate blindly.

---

## Blue-Green Infrastructure Changes

Used when:
- Major infra changes are required
- Downtime is unacceptable

Terraform approach:
1. Create parallel infrastructure
2. Switch traffic
3. Validate
4. Destroy old infra

Terraform supports blue-green **when designed correctly**.

---

## Importing Existing Infrastructure (Reality Check)

### When Import Is Needed
- Legacy infrastructure exists
- Manual resources need Terraform control

### Import Workflow
1. Write matching Terraform config
2. Import resource
3. Validate plan output

⚠️ Import does NOT generate code automatically.

---

## Multi-Environment & Account Strategy

Production-grade strategy:
- Separate AWS accounts per environment
- Separate Terraform state
- Separate CI/CD pipelines

Never mix prod and non-prod state.

---

## Real Incident Case Studies

### Incident 1: Wrong Account Applied
Root cause:
- Same credentials used everywhere

Fix:
- Account-level isolation
- CI/CD role enforcement

---

### Incident 2: Accidental Database Deletion
Root cause:
- Missing `prevent_destroy`

Fix:
- Lifecycle protection
- Approval gates

---
