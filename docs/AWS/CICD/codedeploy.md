---
sidebar_position: 5
title: AWS CodeDeploy
---

# AWS CodeDeploy

Deploying code safely is the **most risky part** of software delivery.
AWS CodeDeploy automates deployments and helps you release changes **without downtime**.

CodeDeploy focuses on **how code is deployed**, not how it is built.

---

## What Is AWS CodeDeploy? (Simple Explanation)

AWS CodeDeploy:
- Automates application deployments
- Deploys to EC2, ECS, Lambda, and on‑premises
- Supports multiple deployment strategies

In simple terms:
> **CodeDeploy = automated and controlled deployments**

---

## Why CodeDeploy Exists

Manual deployments cause:
- Downtime
- Human errors
- Rollback difficulties

CodeDeploy provides:
- Automated rollouts
- Health checks
- Rollback mechanisms

---

## Supported Deployment Targets

CodeDeploy supports:
- EC2 / On‑premises instances
- Amazon ECS
- AWS Lambda

Each target has **different deployment behavior**.

---

## Deployment Strategies

### In‑Place Deployment
- Application is updated on existing instances
- Instances go offline briefly
- Simpler, but riskier

Used for:
- Small environments
- Non‑critical apps

---

### Blue/Green Deployment
- New version deployed alongside old version
- Traffic is switched after validation
- Easy rollback

Used for:
- Production systems
- Zero‑downtime deployments

---

## Deployment Groups

A deployment group:
- Defines **where** to deploy
- Contains instances or services
- Defines deployment settings

It controls:
- Rollout speed
- Health checks
- Failure behavior

---

## appspec.yml (Very Important)

`appspec.yml` defines:
- Deployment lifecycle hooks
- Files to copy
- Scripts to run

It lives:
- In the root of the application package

---

## appspec.yml Example (EC2)

```yaml
version: 0.0
os: linux
files:
  - source: /
    destination: /var/www/app
hooks:
  BeforeInstall:
    - location: scripts/before_install.sh
  AfterInstall:
    - location: scripts/after_install.sh
  ApplicationStart:
    - location: scripts/start.sh
```

---

## Lifecycle Hooks

Common hooks:
- BeforeInstall
- AfterInstall
- ApplicationStart
- ValidateService

Hooks allow:
- Custom deployment logic
- Health validation

---

## Rollbacks and Monitoring

CodeDeploy supports:
- Automatic rollback on failure
- Integration with CloudWatch alarms

This ensures:
- Failed deployments don’t stay live

---

## Security in CodeDeploy

Security features:
- IAM service roles
- Encrypted artifacts (S3 + KMS)
- Instance profiles for EC2

Best practice:
- Least privilege roles

---

## Common Beginner Mistakes

- No health checks
- In‑place deployment for critical apps
- Not testing rollback
- Overly complex scripts

These mistakes cause:
- Production outages

---

## Interview Tip

If asked:
> “How do you deploy applications in AWS safely?”

Strong answer:
> By using AWS CodeDeploy with blue/green deployments and automatic rollback.

---

## Key Takeaways

- CodeDeploy automates deployments
- Supports EC2, ECS, Lambda
- Blue/green is safest strategy
- appspec.yml controls deployments
- Rollback is built‑in

---

📌 **Next:** AWS CodePipeline
