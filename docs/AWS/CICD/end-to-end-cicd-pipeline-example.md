---
sidebar_position: 7
title: End-to-End CI/CD Pipeline Example
---

# End-to-End CI/CD Pipeline Example

This guide ties **all AWS CI/CD services together** into a single, real-world pipeline.
You’ll see how CodeCommit, CodeBuild, CodeDeploy, and CodePipeline work **as one system**.

Goal:
> **Automatically deploy code to EC2 when a developer commits changes**

---

## Architecture Overview

Pipeline flow:

1. Developer pushes code to CodeCommit
2. CodePipeline detects the change
3. CodeBuild builds and tests the application
4. CodeDeploy deploys the app to EC2
5. Application is validated automatically

This is a **standard production pattern**.

---

## Prerequisites

Before creating the pipeline:

- EC2 instances with CodeDeploy agent installed
- IAM roles for CodeBuild, CodeDeploy, and CodePipeline
- S3 bucket for artifacts
- Application code in CodeCommit

---

## Step 1: Source Stage (CodeCommit)

Source stage:
- Repository: CodeCommit
- Trigger: Commit to main branch

What happens:
- Pipeline pulls source code
- Creates source artifact

Best practice:
- Protect main branch
- Use pull requests

---

## Step 2: Build Stage (CodeBuild)

Build stage:
- Uses CodeBuild project
- Reads buildspec.yml

Typical tasks:
- Install dependencies
- Run tests
- Package application

Output:
- Build artifact stored in S3

---

## Sample buildspec.yml

```yaml
version: 0.2

phases:
  install:
    commands:
      - yum install -y httpd
  build:
    commands:
      - echo "Build successful"

artifacts:
  files:
    - '**/*'
```

---

## Step 3: Deploy Stage (CodeDeploy)

Deploy stage:
- Uses CodeDeploy application and deployment group
- Targets EC2 instances

Deployment strategy:
- In-place (simple)
- Blue/Green (recommended for prod)

CodeDeploy:
- Copies files
- Runs lifecycle hooks
- Validates application

---

## Sample appspec.yml

```yaml
version: 0.0
os: linux
files:
  - source: /
    destination: /var/www/html
hooks:
  ApplicationStart:
    - location: scripts/start.sh
  ValidateService:
    - location: scripts/validate.sh
```

---

## Step 4: Manual Approval (Optional)

Add manual approval:
- Before production deployment
- For compliance and safety

Approval:
- Pauses pipeline
- Requires human confirmation

---

## Monitoring the Pipeline

Monitor using:
- CodePipeline console
- CloudWatch Logs
- CodeDeploy deployment status

Always:
- Investigate failures
- Fix root cause
- Retry pipeline

---

## Rollback Scenario

If deployment fails:
- CodeDeploy triggers rollback
- Previous version is restored
- Pipeline reports failure

This prevents:
- Broken production releases

---

## Security Best Practices

- Least privilege IAM roles
- Encrypt artifacts with KMS
- No hardcoded secrets
- Enable CloudTrail logging

---

## Common Beginner Mistakes

- No automated tests
- Skipping approval for prod
- Poor rollback planning
- Overloading build stage

---

## Interview Tip

If asked:
> “Explain an AWS CI/CD pipeline.”

Strong answer:
> CodeCommit stores code, CodePipeline orchestrates the flow, CodeBuild builds and tests, and CodeDeploy deploys safely to EC2.

---

## Key Takeaways

- CI/CD pipelines automate delivery
- CodePipeline connects all stages
- CodeBuild handles CI
- CodeDeploy handles CD
- End-to-end automation reduces risk

---

📌 **Next:** CI/CD Best Practices and Summary
