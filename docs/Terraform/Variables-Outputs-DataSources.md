---
sidebar_position: 4
---

# Variables, Outputs & Data Sources

This phase explains **how Terraform becomes flexible, reusable, and environment-aware**.
Without mastering these concepts, Terraform code quickly becomes hardcoded and unmaintainable.

---

## Why Variables Are Fundamental in Terraform

In real infrastructure:
- Architecture stays mostly the same
- Values change across environments
- Hardcoding values causes duplication and errors

Variables allow you to:
- Reuse the same code
- Change behavior per environment
- Separate **configuration logic** from **data**

Terraform without variables is not production-ready.

---

## Input Variables – How They Really Work

An input variable is a **parameter** that Terraform resolves at runtime.

### Basic Variable Definition
```hcl
variable "instance_type" {
  description = "EC2 instance type"
  type        = string
  default     = "t3.micro"
}
```

Terraform evaluates variables **before planning**.

---

## Variable Resolution Order (Very Important)

Terraform resolves variable values in this order (highest to lowest priority):

1. CLI arguments (`-var`, `-var-file`)
2. Environment variables (`TF_VAR_name`)
3. `terraform.tfvars`
4. `*.auto.tfvars`
5. Variable defaults

Understanding this prevents **unexpected values in production**.

---

## Variable Types – Why Strong Typing Matters

Terraform supports:
- string
- number
- bool
- list
- map
- object
- tuple

Strong typing:
- Prevents invalid values
- Catches errors early
- Improves readability

### Object Variable Example
```hcl
variable "ec2_config" {
  type = object({
    instance_type = string
    volume_size   = number
  })
}
```

---

## terraform.tfvars – Environment Separation

`terraform.tfvars` is used to supply values **without changing code**.

Example:
```hcl
instance_type = "t3.large"
```

Best practice:
- One tfvars per environment
- Never commit secrets

---

## Output Values – Why They Exist

Outputs expose information **after Terraform applies infrastructure**.

Outputs are used for:
- Debugging
- Passing data between modules
- CI/CD pipelines

### Output Example
```hcl
output "instance_ip" {
  value = aws_instance.web.public_ip
}
```

Outputs are read-only.

---

## Expressions & Functions – Terraform Logic

Terraform includes many built-in functions.

Examples:
```hcl
upper("prod")
length(var.subnets)
```

Expressions allow conditional behavior.

```hcl
count = var.env == "prod" ? 3 : 1
```

---

## Loops in Terraform – Scaling Resources

### count (Index-Based)
```hcl
resource "aws_instance" "web" {
  count = 2
}
```

Issues:
- Index-based references
- Fragile during changes

---

### for_each (Key-Based – Preferred)
```hcl
resource "aws_instance" "web" {
  for_each = var.instances
}
```

Advantages:
- Stable identifiers
- Safer refactoring

---

## count vs for_each (Interview Favorite)

| count | for_each |
|------|---------|
| Index-based | Key-based |
| Risky for changes | Safe for updates |
| Simple use cases | Real-world usage |

---

## Dynamic Blocks – Advanced Use Case

Dynamic blocks generate nested blocks dynamically.

```hcl
dynamic "ingress" {
  for_each = var.rules
  content {
    from_port = ingress.value.from
    to_port   = ingress.value.to
  }
}
```

Used when block count is unknown.

---

## Data Sources – Reading Existing Infrastructure

Data sources allow Terraform to **query existing resources**.

Terraform does NOT manage their lifecycle.

---

## Resource vs Data Source (Critical Difference)

| Resource | Data Source |
|--------|------------|
| Creates/manages infra | Reads existing infra |
| Appears in state | Read-only state |
| Terraform-owned | External-owned |

---

## Data Source Example (AMI Lookup)

```hcl
data "aws_ami" "amazon_linux" {
  most_recent = true
}
```

Terraform fetches data during `terraform plan`.

---

## Real-World Usage Patterns

- Variables define environment behavior
- Data sources fetch shared infra
- Outputs wire modules together
- for_each scales safely

---

## Common Mistakes

❌ Hardcoding values  
❌ Using count incorrectly  
❌ Storing secrets in tfvars  
❌ Confusing data sources with resources  

---

## Interview Perspective

You must explain:
- Variable resolution order
- count vs for_each
- Resource vs data source
- Why outputs exist

---

## Summary

You now understand:
- Why variables exist
- How Terraform resolves values
- Strong typing benefits
- Outputs and expressions
- Data sources and loops

These concepts make Terraform **reusable and scalable**.

---

➡️ Next: Terraform Modules (Enterprise-Level)
