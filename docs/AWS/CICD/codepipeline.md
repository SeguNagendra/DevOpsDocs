---
sidebar_position: 6
title: AWS CodePipeline
---

# AWS CodePipeline

CI/CD pipelines are not about individual tools — they are about **orchestration**.
AWS CodePipeline is the service that **connects all CI/CD stages into one automated workflow**.

If CI/CD is a factory,
👉 **CodePipeline is the conveyor belt**.

---

## What Is AWS CodePipeline? (Simple Explanation)

AWS CodePipeline:
- Orchestrates CI/CD workflows
- Connects source, build, test, and deploy stages
- Is event-driven and fully managed

In simple terms:
> **CodePipeline = pipeline coordinator, not a builder or deployer**

---

## Why CodePipeline Exists

Without orchestration:
- Builds and deployments are disconnected
- Manual steps cause delays
- Visibility is poor

CodePipeline provides:
- End-to-end automation
- Visual pipeline stages
- Faster feedback loops

---

## Core Concepts in CodePipeline

Key components:
- Pipeline
- Stage
- Action
- Artifact

Understanding these removes most confusion.

---

## Pipeline

A pipeline:
- Is the top-level workflow
- Represents the entire CI/CD process

Example:
- Source → Build → Test → Deploy

---

## Stage

A stage:
- Groups related actions
- Represents a logical phase

Common stages:
- Source
- Build
- Deploy
- Approval

---

## Action

An action:
- Performs a task in a stage
- Integrates with a service

Examples:
- Source action (CodeCommit)
- Build action (CodeBuild)
- Deploy action (CodeDeploy)

---

## Artifacts

Artifacts:
- Output of one stage
- Input to the next stage
- Stored in S3

Examples:
- Source code ZIP
- Build output package

---

## How CodePipeline Works (Flow)

Typical flow:
1. Code is committed
2. Pipeline is triggered automatically
3. Build and tests run
4. Deployment happens
5. Status is reported

All steps are automated.

---

## Manual Approval Actions

CodePipeline supports:
- Manual approval stages

Used for:
- Production deployments
- Compliance requirements

Approval adds:
- Human control without breaking automation

---

## Integrations Supported

CodePipeline integrates with:
- CodeCommit
- CodeBuild
- CodeDeploy
- CloudFormation
- Lambda
- Third-party tools

---

## Security in CodePipeline

Security features:
- IAM roles per pipeline
- Encrypted artifacts (S3 + KMS)
- Audit logs via CloudTrail

Best practice:
- Least privilege per stage

---

## Common Beginner Mistakes

- Trying to run builds in CodePipeline
- No approval for production
- Poor artifact naming
- Overcomplicated pipelines

These mistakes cause:
- Confusion
- Failed deployments

---

## Interview Tip

If asked:
> “What does CodePipeline do?”

Strong answer:
> CodePipeline orchestrates CI/CD stages by connecting source, build, and deploy services into an automated workflow.

---

## Key Takeaways

- CodePipeline orchestrates CI/CD workflows
- Stages organize pipeline logic
- Actions perform tasks
- Artifacts flow between stages
- Central to AWS CI/CD automation

---

📌 **Next:** End-to-End CI/CD Pipeline Example
