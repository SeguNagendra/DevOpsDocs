---
sidebar_position: 7
---

# Terraform with AWS

This chapter explains **how Terraform is actually used with AWS in real production environments**.
AWS + Terraform is the most common combination in DevOps roles, so this phase is intentionally detailed.

Terraform here is not about syntax — it is about **architecture, safety, and scale**.

---

## Why AWS + Terraform Is the Industry Standard

Terraform is widely used with AWS because:
- AWS provider is mature and stable
- AWS services map well to Terraform resources
- Multi-account and multi-environment patterns are well supported
- Strong module ecosystem exists

In real companies:
> **Terraform is the default way to provision AWS infrastructure**

---

## AWS Provider – How Authentication Really Works

Terraform never stores AWS credentials itself.

Terraform reads credentials in this order:
1. Environment variables
2. AWS CLI config
3. IAM Role (EC2 / EKS)
4. CI/CD assumed roles

### Provider Configuration
```hcl
provider "aws" {
  region = var.aws_region
}
```

### Golden Rule
❌ Never hardcode credentials  
❌ Never commit credentials  

Use IAM roles wherever possible.

---

## AWS Account & Environment Strategy (Critical)

Production-grade AWS setups use:
- Separate AWS accounts per environment
- Separate Terraform state per environment
- Separate CI/CD pipelines

Example:
```
aws-org/
├── dev-account
├── stage-account
└── prod-account
```

This provides **blast-radius isolation**.

---

## VPC – The Networking Foundation

Almost every real AWS environment uses a **custom VPC**.

Terraform-managed VPC includes:
- VPC
- Public & private subnets
- Route tables
- Internet Gateway
- NAT Gateway

### Best Practice
👉 Use a **VPC module**, not raw resources.

Why:
- Networking is complex
- Mistakes are expensive
- Modules encode best practices

---

## Security Groups – Stateful Firewalls

Security groups control network traffic.

Terraform manages:
- Ingress rules
- Egress rules
- Associations

### Common Pattern
- ALB SG allows internet
- App SG allows only ALB
- DB SG allows only app

Never use `0.0.0.0/0` blindly.

---

## EC2 with Terraform – Real Pattern

EC2 instances are rarely standalone.

Typical dependencies:
- AMI (via data source)
- Subnet
- Security group
- IAM role
- User data

```hcl
resource "aws_instance" "app" {
  ami           = data.aws_ami.amazon_linux.id
  instance_type = var.instance_type
  subnet_id     = module.vpc.private_subnets[0]
}
```

Terraform handles infrastructure — not application deployment.

---

## Load Balancer & Auto Scaling (Production Setup)

Production workloads use:
- Application Load Balancer
- Auto Scaling Groups
- Launch Templates

Terraform manages:
- ALB
- Target groups
- Listener rules
- ASG scaling policies

### Lifecycle Rules Matter
Use `create_before_destroy` to avoid downtime.

---

## IAM with Terraform (Very Sensitive)

Terraform commonly manages:
- IAM roles
- IAM policies
- Instance profiles

IAM best practices:
- Least privilege
- Small policies
- Clear ownership

Never destroy critical IAM resources casually.

---

## S3 – More Than Storage

S3 is used for:
- Application data
- Logs
- Terraform remote state

Terraform manages:
- Buckets
- Encryption
- Versioning
- Policies

Always protect production buckets with:
```hcl
lifecycle {
  prevent_destroy = true
}
```

---

## RDS – Databases with Care

Databases require extreme caution.

Terraform should:
- Create RDS
- Configure backups
- Configure networking

Terraform should NOT:
❌ Manage database data  
❌ Run migrations  

Always enable:
- Backups
- Multi-AZ (when needed)
- prevent_destroy

---

## EKS – High-Level Terraform Usage

Terraform is used to:
- Create EKS clusters
- Manage node groups
- Configure IAM

Terraform is NOT used to:
- Deploy Kubernetes workloads

Kubernetes manifests live elsewhere (Helm, ArgoCD).

---

## Remote State in AWS (Standard Pattern)

Typical setup:
- S3 for state storage
- DynamoDB for locking

This ensures:
- Team collaboration
- Safe concurrent usage
- Auditability

---

## Multi-Environment Layout (Recommended)

```
terraform/
└── env/
    ├── dev/
    ├── stage/
    └── prod/
```

Each environment:
- Uses same modules
- Has separate state
- Uses different variables

Avoid workspaces for large AWS setups.

---

## Real-World Failure Scenarios

Common outages:
- Applying to wrong AWS account
- Shared state between envs
- Missing lifecycle protections
- Over-permissive IAM

Terraform reduces risk **only when used correctly**.

---

## Interview Perspective

You should confidently explain:
- How Terraform authenticates to AWS
- Why multi-account strategy matters
- How ALB + ASG is provisioned
- Why state is stored in S3

---

## Summary

You now understand:
- How Terraform integrates with AWS
- Real production architecture patterns
- IAM, networking, compute, and storage
- Environment and account isolation
- Safety mechanisms for AWS infrastructure

Terraform + AWS mastery is about **architecture discipline**, not commands.

---

➡️ Next: Terraform Best Practices & Security (Complete & Deep)
