---
sidebar_position: 3
---

# Terraform State Management

Terraform **state** is the backbone of how Terraform understands, tracks, and manages infrastructure.
This phase is **one of the most important** for real-world usage and interviews.

If you understand state well, you understand Terraform.

---

## What is Terraform State?

Terraform state is a **record of infrastructure resources** that Terraform manages.
It is stored in a file called:

```
terraform.tfstate
```

This file maps:
- Terraform resources ➝ real cloud resources
- Resource IDs
- Attributes and metadata

### Why Terraform Needs State
Terraform does NOT query the cloud every time to understand everything.
Instead, it:
1. Reads the **state file**
2. Compares it with your `.tf` code
3. Compares both with real infrastructure

This comparison is called **state reconciliation**.

---

## Desired State vs Current State

- **Desired State** → What you write in `.tf` files
- **Current State** → What exists in the cloud
- **Terraform State** → Terraform’s memory of the infrastructure

Terraform always tries to make:
```
Current State == Desired State
```

---

## Local State

By default, Terraform stores state locally.

📁 Example:
```
terraform.tfstate
terraform.tfstate.backup
```

### Problems with Local State
- Not shareable between team members
- No locking (race conditions)
- Risk of accidental deletion
- Unsafe for production

👉 Local state is **ONLY acceptable for learning or experiments**.

---

## Remote State (Production Standard)

Remote state stores Terraform state in a remote backend.

### Common Remote Backends
- AWS S3
- Azure Blob Storage
- Google Cloud Storage
- Terraform Cloud

### Benefits of Remote State
- Centralized state
- Team collaboration
- State locking
- Better security

---

## Backend vs Provider (Very Important)

| Backend | Provider |
|------|--------|
| Stores state | Creates resources |
| Initialized first | Initialized after backend |
| One backend per config | Multiple providers allowed |
| No resource creation | Talks to cloud APIs |

This distinction is a **very common interview question**.

---

## Remote State with AWS S3 (Example)

```hcl
terraform {
  backend "s3" {
    bucket         = "terraform-state-prod"
    key            = "vpc/terraform.tfstate"
    region         = "us-east-1"
    dynamodb_table = "terraform-locks"
    encrypt        = true
  }
}
```

### What Happens Here?
- State stored in S3
- Locking handled by DynamoDB
- Encryption enabled

---

## State Locking

State locking prevents **multiple users** from modifying infrastructure at the same time.

### Without Locking
- Two engineers run `terraform apply`
- State corruption happens
- Infrastructure becomes inconsistent

### With Locking
- One operation at a time
- Others must wait

DynamoDB is commonly used for locking in AWS.

---

## Terraform State Commands

### List Resources
```bash
terraform state list
```

### Inspect Resource
```bash
terraform state show aws_instance.web
```

### Move Resource
```bash
terraform state mv aws_instance.old aws_instance.new
```

### Remove Resource from State
```bash
terraform state rm aws_instance.test
```

⚠️ Removing from state does **NOT delete** the real resource.

---

## Terraform Import (Real-World Scenario)

Used when infrastructure already exists but Terraform does not manage it.

### Example
```bash
terraform import aws_instance.web i-0123456789abcdef
```

### Important Limitations
- Import does NOT generate `.tf` code
- You must manually write matching configuration
- Complex resources require careful imports

---

## State Migration

State migration occurs when:
- Backend changes
- State location changes

### Example
```bash
terraform init -migrate-state
```

Terraform safely moves state to the new backend.

---

## Infrastructure Drift

**Drift** occurs when infrastructure is modified outside Terraform.

Example:
- EC2 resized manually from AWS Console

Terraform detects drift during:
```bash
terraform plan
```

Drift is shown as unexpected changes.

---

## Real-World Best Practices

✅ Always use remote state  
✅ Enable state locking  
✅ Restrict state access (IAM policies)  
✅ Never edit state files manually  
✅ Take state backups  

---

## Common Mistakes

❌ Storing state in Git  
❌ Deleting state files  
❌ Sharing local state across team  
❌ Ignoring state locks  

---

## Interview Tips

You should be able to explain:
- Why Terraform needs state
- Backend vs provider difference
- How state locking works
- What happens during drift

---

## Summary

In this phase, you learned:
- What Terraform state is
- Why it is critical
- Local vs remote state
- State locking & backends
- Importing existing infrastructure
- Drift detection

---

➡️ **Next Phase:** Variables, Outputs & Data Sources
