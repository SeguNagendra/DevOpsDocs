---
sidebar_position: 1
---

# Terraform Fundamentals

This chapter builds the **mental model** required to truly understand Terraform.
If this foundation is weak, everything later (state, modules, CI/CD) will feel confusing.

Read this slowly. Terraform is simple **once you think the way Terraform thinks**.

---

## What is Terraform (Real Explanation)

Terraform is an **Infrastructure as Code (IaC)** tool created by HashiCorp.

But practically, Terraform is:
> A **state-driven infrastructure reconciliation engine**

This means:
- You describe the **desired state** of infrastructure
- Terraform compares it with the **current state**
- Terraform calculates the **difference**
- Terraform executes only what is required to fix that difference

Terraform is **not a scripting tool**.
It is a **planner + executor**.

---

## The Problem Terraform Solves (Why It Exists)

### Before Terraform
Infrastructure was:
- Created manually in cloud consoles
- Different across environments
- Poorly documented
- Hard to reproduce

Typical problems:
- “Works in dev but not prod”
- No rollback for infra changes
- No audit trail

### With Terraform
Infrastructure becomes:
- Version controlled
- Reproducible
- Reviewable
- Automated

Terraform treats **infrastructure like application code**.

---

## Infrastructure as Code (IaC) – Properly Explained

IaC means:
- Infrastructure is defined in files
- Those files live in Git
- Changes follow pull request workflows

Terraform uses a **declarative model**.

Declarative means:
> You define *what you want*, not *how to do it*

You never say:
❌ “Create subnet, then route table, then attach IGW”

You say:
✅ “This is my infrastructure”

Terraform figures out the rest.

---

## Declarative vs Imperative (Critical Difference)

### Imperative (Scripts)
- Step-by-step instructions
- Order matters
- Hard to rollback

### Declarative (Terraform)
- End-state focused
- Order is computed automatically
- Safe to re-run

Terraform can be executed **multiple times safely**.

This property is called **idempotency**.

---

## Terraform vs Other Tools (Mental Model)

### Terraform vs Ansible
- Terraform: infrastructure lifecycle
- Ansible: configuration inside servers

Terraform creates servers.
Ansible configures servers.

They are **complementary**, not competitors.

---

### Terraform vs CloudFormation
- Terraform: multi-cloud, faster innovation
- CloudFormation: AWS-only, tightly integrated

Terraform is preferred when:
- Teams use multiple clouds
- Strong modularity is required

---

## Terraform Architecture (Internal View)

Terraform is composed of multiple parts working together.

---

### Terraform Core

Terraform Core:
- Reads `.tf` files
- Loads providers
- Builds dependency graph
- Reads state
- Creates execution plan
- Applies changes

Terraform Core does **not** talk to AWS directly.

---

### Providers (How Terraform Talks to Clouds)

Providers are **plugins**.

Their job:
- Authenticate to cloud APIs
- Translate Terraform instructions into API calls
- Read and create resources

Examples:
- AWS provider
- Azure provider
- Kubernetes provider

Without providers, Terraform does nothing.

---

## Terraform State (High-Level Introduction)

Terraform maintains a **state file**.

The state file:
- Maps Terraform resources to real resources
- Stores resource IDs
- Stores metadata

Terraform state is:
> Terraform’s memory of the infrastructure

⚠️ State files are critical and must be protected.

(State is explained deeply in Phase 3.)

---

## How Terraform Thinks (Very Important)

Terraform always answers three questions:

1. What do I want? (configuration)
2. What do I have? (state)
3. What exists? (real infrastructure)

Terraform compares these and produces a **plan**.

Nothing is changed until you approve the plan.

---

## Terraform Workflow (Internal Mechanics)

### Step 1: Write Configuration
You define resources in `.tf` files.

Terraform loads **all `.tf` files in a directory together**.

File order does NOT matter.

---

### Step 2: terraform init

What actually happens:
- Backend is initialized
- Providers are downloaded
- Provider versions are locked

Without init, Terraform cannot proceed.

---

### Step 3: terraform plan

Terraform:
- Reads state
- Queries providers
- Compares desired vs current state
- Produces an execution plan

Plan answers:
- What will be created
- What will change
- What will be destroyed

---

### Step 4: terraform apply

Terraform:
- Executes the plan
- Applies changes in correct order
- Updates state

Terraform does **exactly what the plan shows**.

---

## Why terraform destroy Exists

Terraform destroy:
- Uses state to find managed resources
- Deletes them safely

Destroy is powerful and dangerous.

Never run destroy on production casually.

---

## Installing Terraform (Conceptual)

Terraform is a **single binary**.

Installation means:
- Download binary
- Place in PATH
- Verify version

```bash
terraform version
```

No agents. No servers.

---

## Terraform CLI Commands (Why They Matter)

```bash
terraform init      # prepares environment
terraform plan      # safety preview
terraform apply     # execute changes
terraform destroy   # remove infra
terraform validate  # syntax check
terraform fmt       # formatting
```

Each command exists for **safety**, not convenience.

---

## Real-World Usage Pattern

In real teams:
- Terraform code lives in Git
- Changes go through pull requests
- terraform plan is reviewed
- terraform apply runs via CI/CD

Humans approve. Machines execute.

---

## Common Beginner Mistakes (Why They Hurt)

❌ Treating Terraform like a script  
❌ Editing state manually  
❌ Running apply on prod locally  
❌ Skipping plan review  

These mistakes cause **outages**.

---

## Interview Mindset

Interviewers look for:
- Conceptual clarity
- Correct mental model
- Safety awareness

Be able to explain:
- Why Terraform needs state
- Declarative vs imperative
- Terraform workflow internally

---

## Summary

You now understand:
- Why Terraform exists
- How Terraform thinks
- What problems it solves
- How Terraform executes changes

This understanding is **non-negotiable** for mastering Terraform.

---

➡️ Next: Terraform Core Concepts & Configuration (Deep)
