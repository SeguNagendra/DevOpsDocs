---
sidebar_position: 2
---

# Terraform Core Concepts & Configuration

This chapter explains **how Terraform reads, understands, and processes your code**.
Most Terraform confusion comes from not understanding this internal behavior.

Think of this phase as learning **Terraform’s brain**.

---

## How Terraform Reads Configuration Files

Terraform does NOT execute files line by line.

Instead:
- Terraform loads **all `.tf` files in a directory at once**
- It merges them into a **single configuration**
- File names and order do **not** matter

This means:
❌ `main.tf` is not special  
❌ Order of resources across files is irrelevant  

Terraform reasons about the **whole configuration**, not files.

---

## Terraform Configuration Language (HCL) – Deep Understanding

Terraform uses **HCL (HashiCorp Configuration Language)**.

HCL is designed to:
- Be human-readable
- Be machine-parseable
- Represent infrastructure cleanly

### Core Building Blocks

```hcl
<block_type> "<label1>" "<label2>" {
  argument = value
}
```

Example:
```hcl
resource "aws_instance" "web" {
  instance_type = "t3.micro"
}
```

Blocks describe **intent**, not execution steps.

---

## Blocks, Arguments, and Attributes

### Block
Defines a logical object (resource, provider, variable).

### Argument
Inputs you provide.

```hcl
instance_type = "t3.micro"
```

### Attribute
Values Terraform learns after creation.

```hcl
aws_instance.web.public_ip
```

Understanding this difference is critical.

---

## Providers – The Translation Layer

Terraform Core cannot talk to AWS, Azure, or GCP.

Providers:
- Authenticate with cloud APIs
- Translate Terraform logic into API calls
- Read and manage resources

Think of providers as **drivers**.

---

## Provider Configuration (Best Practice)

```hcl
provider "aws" {
  region = var.region
}
```

Key rules:
- Providers are configured in the **root module**
- Child modules should NOT hardcode providers
- Credentials are never stored in code

---

## Required Providers & Version Locking (CRITICAL)

Terraform must know:
- Which provider to use
- Which version is allowed

```hcl
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 5.0"
    }
  }
}
```

### Why This Is Non-Negotiable
- Providers introduce breaking changes
- CI/CD pipelines rely on determinism
- Production stability depends on version pinning

---

## Terraform Version Constraints

```hcl
terraform {
  required_version = ">= 1.5.0"
}
```

This ensures:
- Team consistency
- Predictable behavior
- Safer upgrades

---

## Resources – Real Infrastructure Objects

Resources represent **actual cloud components**.

```hcl
resource "aws_s3_bucket" "logs" {
  bucket = "company-logs-prod"
}
```

Terraform tracks resources as:
```
resource_type.resource_name
```

This mapping is stored in state.

---

## Resource Lifecycle (High-Level)

Every resource goes through:
1. Create
2. Read
3. Update
4. Delete

Providers implement this lifecycle using APIs.

---

## Terraform Dependency Graph (Core Concept)

Terraform automatically builds a **dependency graph**.

Dependencies are inferred when:
```hcl
subnet_id = aws_subnet.public.id
```

Terraform:
- Knows subnet must exist first
- Orders execution safely
- Prevents race conditions

This is why Terraform is reliable at scale.

---

## Terraform Workflow – Internal Execution Model

### terraform init
Internally:
- Backend initialized
- Providers downloaded
- Plugins cached
- Versions locked

Without init → nothing works.

---

### terraform plan
Terraform:
- Reads configuration
- Reads state
- Queries provider APIs
- Computes differences
- Produces execution plan

Plan is a **safety contract**.

---

### terraform apply
Terraform:
- Executes the plan
- Applies changes in dependency order
- Updates state after success

Terraform never partially commits silently.

---

## Why Re-Running Terraform Is Safe

Terraform is **idempotent**.

Running apply multiple times:
- Does NOT recreate resources
- Only fixes drift
- Maintains desired state

This is a core design principle.

---

## Real-World Configuration Pattern

Typical repo:
```
.
├── providers.tf
├── main.tf
├── variables.tf
├── outputs.tf
```

Files are for **humans**, not Terraform.

---

## Common Misconceptions (Very Important)

❌ File order controls execution  
❌ Terraform is procedural  
❌ Providers create resources automatically  
❌ Latest versions are always safe  

All false.

---

## Interview Perspective

You should confidently explain:
- How Terraform loads `.tf` files
- Why file order does not matter
- Provider vs resource vs backend
- Why version pinning is critical

---

## Summary

You now understand:
- How Terraform reads configuration
- HCL structure deeply
- Providers and versioning
- Dependency graph logic
- Internal workflow execution

This knowledge prevents **most beginner and mid-level mistakes**.

---

➡️ Next: Terraform State Management (Deep Dive)
