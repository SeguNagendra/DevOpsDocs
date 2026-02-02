---
sidebar_position: 6
title: Modular CloudFormation and Nested Stacks
---

# Modular CloudFormation and Nested Stacks

As infrastructure grows, **large single CloudFormation templates become hard to manage**.
Modular CloudFormation solves this by **splitting infrastructure into reusable, manageable components**.

This document explains **nested stacks and modular design patterns** used in real projects.

---

## Why Modular CloudFormation?

Problems with monolithic templates:
- Hard to read
- Difficult to update safely
- Poor reusability
- High blast radius

Modular design provides:
- Reusability
- Isolation
- Easier maintenance

---

## What Is a Nested Stack?

A nested stack:
- Is a CloudFormation stack created by another stack
- Uses a separate template
- Is managed as part of the parent stack

In simple terms:
> **Nested stacks = stacks inside stacks**

---

## Parent vs Child Stacks

- **Parent stack**: Orchestrates infrastructure
- **Child stack**: Defines a specific component

Example components:
- VPC stack
- Security stack
- Application stack

---

## Basic Nested Stack Example

```yaml
Resources:
  VPCStack:
    Type: AWS::CloudFormation::Stack
    Properties:
      TemplateURL: https://s3.amazonaws.com/mybucket/vpc.yaml
```

Each child stack:
- Has its own lifecycle
- Can output values

---

## Passing Values Between Stacks

Use Outputs and Parameters:

Child stack:
```yaml
Outputs:
  VpcId:
    Value: !Ref MyVPC
```

Parent stack:
```yaml
VpcId: !GetAtt VPCStack.Outputs.VpcId
```

This enables:
- Loose coupling

---

## When to Use Nested Stacks

Nested stacks are ideal for:
- Shared infrastructure components
- Reusable modules
- Large environments

Avoid:
- Over-nesting (too many layers)

---

## Modular Design Patterns

Common modules:
- Network (VPC, subnets)
- Security (IAM, SGs)
- Compute (ASG, EC2)
- Databases

Modules should:
- Do one thing well

---

## Versioning Nested Templates

Best practices:
- Store templates in S3
- Version templates
- Avoid breaking changes

Versioning prevents:
- Accidental regressions

---

## Nested Stacks vs Cross-Stack References

Nested stacks:
- Tightly coupled
- Managed together

Cross-stack references:
- Loosely coupled
- Separate lifecycles

Choose based on:
- Dependency strength

---

## Limits and Considerations

CloudFormation limits:
- Max 60 nested stacks
- Template size limits

Plan design:
- To avoid hitting limits

---

## Common Beginner Mistakes

- Giant monolithic templates
- Hardcoded values
- No module boundaries
- No documentation

These reduce maintainability.

---

## Interview Tip

If asked:
> “How do you manage large CloudFormation templates?”

Strong answer:
> By using modular templates and nested stacks to separate concerns and improve reuse.

---

## Key Takeaways

- Modular design improves scalability
- Nested stacks enable reuse
- Outputs connect modules
- Versioning is critical
- Balance modularity with simplicity

---

📌 **Next:** AWS CDK vs CloudFormation vs Terraform
