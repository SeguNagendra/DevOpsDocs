---
sidebar_position: 5
---

# Terraform Modules

Modules are **the foundation of professional Terraform usage**.
Any real-world Terraform codebase that is not toy-sized relies heavily on modules.

Think of modules as **functions for infrastructure**.

---

## Why Modules Exist (Real Problems They Solve)

Without modules, teams face:
- Massive duplication across environments
- Copy–paste errors
- Inconsistent infrastructure standards
- Painful refactoring

Modules solve these problems by:
- Encapsulating infrastructure logic
- Enforcing standards
- Enabling reuse at scale

If you are not using modules, you are **not using Terraform correctly**.

---

## What Exactly Is a Module?

A Terraform module is:
> A **directory containing Terraform configuration files**

Nothing more. Nothing less.

Terraform treats:
- The current directory → **Root module**
- Any referenced directory → **Child module**

---

## Root Module vs Child Module (Very Important)

### Root Module
- Entry point of Terraform
- Contains backend & provider configuration
- Calls child modules
- Controls environments

### Child Module
- Reusable infrastructure component
- Accepts inputs via variables
- Exposes outputs
- Does NOT contain environment-specific logic

---

## How Terraform Evaluates Modules

Terraform:
1. Loads root module
2. Resolves module sources
3. Passes input variables
4. Evaluates child modules
5. Merges outputs into dependency graph

Modules are resolved **before planning**.

---

## Recommended Module Directory Structure

```
modules/
├── vpc/
│   ├── main.tf
│   ├── variables.tf
│   ├── outputs.tf
│   └── README.md
├── compute/
└── database/
```

Root module:
```
env/prod/
├── main.tf
├── providers.tf
├── backend.tf
└── terraform.tfvars
```

This structure scales cleanly.

---

## Creating a Simple Child Module (EC2 Example)

### modules/compute/main.tf
```hcl
resource "aws_instance" "this" {
  ami           = var.ami
  instance_type = var.instance_type
  subnet_id     = var.subnet_id
}
```

### variables.tf
```hcl
variable "ami" {}
variable "instance_type" {}
variable "subnet_id" {}
```

---

## Calling a Module from Root Module

```hcl
module "web" {
  source        = "../../modules/compute"
  ami           = data.aws_ami.amazon_linux.id
  instance_type = "t3.micro"
  subnet_id     = module.vpc.public_subnets[0]
}
```

Terraform treats module calls like **function calls**.

---

## Module Inputs – Design Guidelines

Good module inputs:
- Are explicit
- Are typed
- Have descriptions
- Avoid environment-specific naming

Bad module inputs:
❌ `is_prod`  
❌ `environment_name`  
❌ Hardcoded ARNs  

---

## Module Outputs – When & Why

Outputs should:
- Expose only what is needed
- Be stable
- Avoid leaking sensitive data

Example:
```hcl
output "instance_id" {
  value = aws_instance.this.id
}
```

Outputs are the **contract** between modules.

---

## Module Versioning (NON-NEGOTIABLE)

Never use unversioned modules in production.

### Git-Based Versioning
```hcl
module "vpc" {
  source = "git::https://github.com/org/vpc.git?ref=v1.3.0"
}
```

### Registry Module Versioning
```hcl
module "vpc" {
  source  = "terraform-aws-modules/vpc/aws"
  version = "~> 5.0"
}
```

Versioning ensures:
- Predictability
- Safe upgrades
- Rollbacks

---

## Terraform Registry Modules

The public registry provides:
- Pre-built, tested modules
- Documentation
- Versioning

Use registry modules when:
- Infrastructure is standard
- Module is actively maintained

Avoid registry modules when:
- Heavy customization is required
- Security policies are strict

---

## Providers Inside Modules (Critical Rule)

Best practice:
- Providers configured in root module
- Passed implicitly to child modules

Why:
- Prevents provider conflicts
- Enables multi-account usage
- Improves reusability

---

## Module Composition Pattern

Large systems are composed using:
- Network module
- Security module
- Compute module
- Database module

Each module has **single responsibility**.

---

## Refactoring with Modules (Real Scenario)

Common scenario:
- Flat Terraform codebase
- Growing complexity

Refactor steps:
1. Identify logical components
2. Extract into modules
3. Use state mv if needed
4. Validate plan carefully

Refactoring is safe when done correctly.

---

## Common Module Anti-Patterns

❌ One giant module  
❌ Too many inputs  
❌ Environment logic inside module  
❌ Copy-pasting instead of versioning  

These destroy maintainability.

---

## Real-World Best Practices

✅ Small focused modules  
✅ Clear inputs & outputs  
✅ Version everything  
✅ Document modules  
✅ Enforce standards  

---

## Interview Perspective

Expect questions like:
- Why modules are needed
- Root vs child modules
- How versioning works
- How teams structure Terraform repos

---

## Summary

You now understand:
- What modules are
- How Terraform evaluates them
- How to design good modules
- Versioning strategies
- Enterprise composition patterns

Modules are **Terraform at scale**.

---

➡️ Next: Advanced Terraform Concepts
