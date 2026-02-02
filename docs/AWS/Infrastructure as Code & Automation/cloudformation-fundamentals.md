---
sidebar_position: 2
title: AWS CloudFormation Fundamentals
---

# AWS CloudFormation – Fundamentals

AWS CloudFormation is the **native Infrastructure as Code (IaC) service** for AWS.
It allows you to define, provision, and manage AWS resources **using declarative templates**.

If you understand CloudFormation, you understand **how AWS wants infrastructure to be built**.

---

## What Is AWS CloudFormation?

AWS CloudFormation:
- Uses templates to define infrastructure
- Provisions resources as a single unit called a *stack*
- Manages lifecycle: create, update, delete

In simple terms:
> **CloudFormation = AWS infrastructure defined as code**

---

## Why Use CloudFormation?

CloudFormation provides:
- Consistency across environments
- Repeatable deployments
- Automatic dependency handling
- Built-in rollback on failure

Manual creation cannot match this reliability.

---

## CloudFormation Core Components

CloudFormation works using:

- Templates
- Stacks
- Resources
- Parameters
- Outputs

These components work together to define infrastructure.

---

## CloudFormation Templates

A template is:
- A JSON or YAML file
- Describes desired AWS resources

Templates are:
- Declarative
- Version-controlled
- Reusable

---

## Stacks

A stack is:
- A running instance of a template
- A collection of AWS resources managed together

Rule:
> **Never modify stack resources manually**

---

## Resources

Resources define:
- What AWS services are created

Examples:
- EC2 instances
- S3 buckets
- IAM roles

Each resource:
- Has a logical ID
- Maps to an AWS service

---

## Parameters

Parameters:
- Make templates reusable
- Accept input values at runtime

Examples:
- Instance type
- Environment name

Avoid:
- Hardcoding values

---

## Outputs

Outputs:
- Export important values
- Enable cross-stack references

Examples:
- VPC ID
- Load balancer DNS name

---

## Template Structure (High Level)

Common sections:
- AWSTemplateFormatVersion
- Description
- Parameters
- Resources
- Outputs

Not all sections are mandatory.

---

## CloudFormation Change Sets

Change sets:
- Show what will change before update
- Prevent unexpected modifications

Best practice:
> **Always review change sets before applying**

---

## Rollback and Failure Handling

If stack creation fails:
- CloudFormation rolls back automatically
- Prevents partial infrastructure

This makes deployments safer.

---

## CloudFormation and IAM

CloudFormation uses:
- Execution roles
- Permissions to create resources

Best practice:
- Use least-privilege roles

---

## Common Beginner Mistakes

- Editing stack resources manually
- No parameters
- No change set review
- Overly large templates

These cause:
- Drift and failures

---

## Interview Tip

If asked:
> “What is AWS CloudFormation?”

Strong answer:
> AWS CloudFormation is an IaC service that provisions AWS resources using declarative templates and manages them as stacks.

---

## Key Takeaways

- CloudFormation is AWS-native IaC
- Templates define desired state
- Stacks manage lifecycle
- Rollbacks improve safety
- Essential for automation

---

📌 **Next:** CloudFormation Template Anatomy
