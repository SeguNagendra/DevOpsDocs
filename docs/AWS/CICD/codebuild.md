---
sidebar_position: 4
title: AWS CodeBuild
---

# AWS CodeBuild

Building and testing code is the **heart of Continuous Integration**.
AWS CodeBuild is a **fully managed build service** that compiles code, runs tests, and produces artifacts.

You don’t manage build servers.
👉 You define **what to build**, AWS handles **how to build it**.

---

## What Is AWS CodeBuild? (Simple Explanation)

AWS CodeBuild:
- Compiles source code
- Runs automated tests
- Packages build artifacts
- Runs in a serverless manner

In simple terms:
> **CodeBuild = serverless build and test service**

---

## Why CodeBuild Exists

Traditional build servers:
- Need patching
- Need scaling
- Break frequently

CodeBuild provides:
- On-demand build environments
- Automatic scaling
- Pay only for build time

---

## How CodeBuild Works (High Level)

Typical flow:
1. CodePipeline or developer triggers build
2. CodeBuild pulls source code
3. Build commands run
4. Artifacts are generated
5. Results are sent back

---

## Build Environment

CodeBuild runs builds inside:
- Managed Docker containers

You can choose:
- Predefined images (Java, Node.js, Python, etc.)
- Custom Docker images

Environment includes:
- OS
- Runtime
- Tools

---

## buildspec.yml (Very Important)

The `buildspec.yml` file defines:
- Build steps
- Commands
- Artifacts

It lives:
- In the root of your repository

---

## buildspec.yml Structure

A typical buildspec has:

- version
- phases
- artifacts
- cache (optional)

---

## Example buildspec.yml

```yaml
version: 0.2

phases:
  install:
    commands:
      - npm install
  build:
    commands:
      - npm run build

artifacts:
  files:
    - '**/*'
```

---

## Build Phases

Common phases:
- install
- pre_build
- build
- post_build

Use cases:
- install dependencies
- run tests
- package code

---

## Build Artifacts

Artifacts are:
- Output files from build
- Stored in S3
- Passed to next pipeline stage

Examples:
- JAR files
- ZIP packages
- Docker images

---

## Environment Variables

CodeBuild supports:
- Plain environment variables
- Secrets from Secrets Manager or Parameter Store

👉 Never hardcode secrets in buildspec.

---

## Build Caching

Caching:
- Speeds up builds
- Reduces repeated downloads

Common caches:
- Dependency directories
- Docker layers

---

## Security in CodeBuild

Security features:
- IAM role for CodeBuild
- Encrypted artifacts (S3 + KMS)
- VPC support for private builds

Best practice:
- Least privilege IAM role

---

## Monitoring Builds

Monitor using:
- CloudWatch Logs
- Build history

Use logs to:
- Debug build failures
- Optimize build times

---

## Common Beginner Mistakes

- Hardcoding secrets
- No build caching
- Overly large artifacts
- Not failing builds on test failures

These mistakes cause:
- Slow pipelines
- Security risks

---

## Interview Tip

If asked:
> “How do you build and test code in AWS?”

Strong answer:
> By using AWS CodeBuild to run automated builds and tests defined in a buildspec.yml file.

---

## Key Takeaways

- CodeBuild is serverless CI build service
- buildspec.yml defines build logic
- Supports caching and artifacts
- Secure via IAM and KMS
- Integrates with CodePipeline

---

📌 **Next:** AWS CodeDeploy
