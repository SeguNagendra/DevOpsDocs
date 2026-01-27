---
sidebar_position: 6
---

# Advanced Terraform Concepts

This chapter explains **how Terraform behaves in complex, real-world situations**.
These concepts are what differentiate **basic Terraform users** from **production-ready engineers**.

---

## Terraform Dependency Graph (How Ordering Really Works)

Terraform does not execute resources in file order.
It builds a **Directed Acyclic Graph (DAG)** of dependencies.

Terraform uses this graph to:
- Determine creation order
- Parallelize safe operations
- Prevent race conditions

---

## Implicit Dependencies (Preferred)

Terraform automatically infers dependencies when one resource references another.

```hcl
subnet_id = aws_subnet.public.id
```

Terraform understands:
- Subnet must exist before EC2
- EC2 depends on subnet

Implicit dependencies keep code clean and safe.

---

## Explicit Dependencies (`depends_on`)

Used only when dependencies are **not visible in code**.

```hcl
depends_on = [aws_iam_role_policy_attachment.attach]
```

### When to Use
- External systems
- Side effects
- Hidden ordering constraints

### When NOT to Use
- As a default
- To “fix” broken design

Overuse leads to fragile graphs.

---

## Lifecycle Meta-Arguments (CRITICAL FOR PRODUCTION)

Lifecycle rules control **how Terraform creates, updates, and destroys resources**.

---

### create_before_destroy

```hcl
lifecycle {
  create_before_destroy = true
}
```

Used when:
- Downtime is unacceptable
- Replacements are risky

Common examples:
- Load balancers
- Auto Scaling Groups

---

### prevent_destroy

```hcl
lifecycle {
  prevent_destroy = true
}
```

Protects:
- Databases
- Critical storage
- Core networking

Terraform will refuse destructive plans.

---

### ignore_changes

```hcl
lifecycle {
  ignore_changes = [tags]
}
```

Used when:
- Attributes are managed outside Terraform
- External systems modify resources

Use carefully to avoid drift blindness.

---

## Provisioners (Why They Are Discouraged)

Provisioners allow running scripts during resource creation.

Types:
- local-exec
- remote-exec

---

### Why Provisioners Are Dangerous

- Run only during creation
- Not idempotent
- Hard to retry
- Break Terraform’s declarative model

Provisioners often cause **partial failures**.

---

### Acceptable Use Cases (Rare)

- One-time bootstrap scripts
- Temporary migration logic

Prefer:
- Cloud-init
- Image baking
- Configuration management tools

---

## Null Resources (Controlled Side Effects)

`null_resource` has no real infrastructure.

```hcl
resource "null_resource" "deploy" {
  triggers = {
    version = var.app_version
  }
}
```

Used to:
- Trigger scripts
- Integrate CI/CD hooks

Not a replacement for bad design.

---

## Terraform Workspaces (Truth vs Marketing)

Workspaces create **multiple state files** for one configuration.

```bash
terraform workspace new dev
terraform workspace select prod
```

---

### What Workspaces Are Good For

- Simple experiments
- Small projects
- Learning environments

---

### What Workspaces Are NOT Good For

- Strong environment isolation
- Multi-account production setups
- Compliance-heavy systems

---

### Preferred Alternative

Folder-based environments:
```
env/dev
env/stage
env/prod
```

This provides clearer separation and safety.

---

## Handling Sensitive Data (Deep Understanding)

Terraform supports sensitive values, but:

Sensitive ≠ Secure

State files may still contain secrets.

---

### Best Practices

- Use secret managers
- Inject secrets at runtime
- Restrict state access
- Avoid outputs for secrets

Terraform should **reference**, not store secrets.

---

## Debugging & Advanced Troubleshooting

### terraform plan
Always inspect plan output carefully.

Look for:
- Replacements
- Unexpected destroys
- Drift

---

### terraform graph

```bash
terraform graph | dot -Tpng > graph.png
```

Useful for:
- Visualizing dependencies
- Debugging complex graphs

---

### Debug Logs

```bash
TF_LOG=TRACE terraform apply
```

Use sparingly.

---

## Real-World Best Practices

✅ Prefer implicit dependencies  
✅ Use lifecycle rules intentionally  
✅ Avoid provisioners  
✅ Treat workspaces carefully  
✅ Protect secrets and state  

---

## Common Advanced Mistakes

❌ Overusing depends_on  
❌ Ignoring lifecycle protections  
❌ Treating Terraform like a script  
❌ Misusing workspaces  

---

## Interview Perspective

You must explain:
- Dependency graph behavior
- Lifecycle rules with examples
- Why provisioners are discouraged
- Workspace limitations

---

## Summary

You now understand:
- How Terraform orders execution
- Lifecycle meta-arguments deeply
- Provisioners and null resources
- Workspace realities
- Debugging techniques

These concepts are **mandatory for senior-level Terraform usage**.

---

➡️ Next: Terraform with AWS (Complete & Deep)
