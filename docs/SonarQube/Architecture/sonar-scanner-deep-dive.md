---
sidebar_position: 6
---

# Sonar Scanner Deep Dive – How Analysis Really Works

Now that we understand SonarQube’s architecture, it’s time to zoom into the **Sonar Scanner**.
Most real-world SonarQube issues happen at the scanner level, so understanding it deeply is critical.

---

## What Exactly Is the Sonar Scanner?

The Sonar Scanner is a **client-side tool** that runs close to your source code.

Its responsibilities are simple but important:
- Read source files
- Apply quality rules locally
- Collect metrics and issues
- Send analysis data to the SonarQube Server

The scanner does **not**:
- Store results
- Decide Quality Gate status
- Keep history

---

## Where the Scanner Runs

Depending on your setup, the scanner can run:
- On a developer’s machine
- Inside a CI/CD pipeline
- On a build server (Jenkins, GitHub Actions, GitLab CI)

Best practice:
> Always run the scanner as part of CI/CD.

---

## Types of Sonar Scanners

SonarQube provides different scanners to fit build ecosystems.

### SonarScanner CLI
- Language-agnostic
- Works with any project
- Requires manual configuration

### Build Tool Scanners
- **Maven Scanner**
- **Gradle Scanner**
- **.NET Scanner**

These integrate directly into build lifecycles and require less configuration.

---

## Scanner Execution Lifecycle

Understanding the lifecycle helps debugging.

1. Scanner starts
2. Project configuration is loaded
3. Source files are detected
4. Rules are applied
5. Results are packaged
6. Data is sent to the server
7. Scanner exits

If the scanner exits successfully, analysis was sent — not necessarily accepted.

---

## Configuration Basics

Scanners are configured using:
- `sonar-project.properties`
- Environment variables
- CI/CD pipeline variables

Key properties:
- Project key
- Organization
- Server URL
- Authentication token

---

## Authentication with Tokens

Scanners authenticate using **tokens**, not passwords.

Best practices:
- Use project-specific tokens
- Store tokens in CI secret managers
- Rotate tokens periodically

Never hardcode tokens in repositories.

---

## Debugging Scanner Issues

When scans fail, enable debug mode:

```
sonar-scanner -X
```

This shows:
- File detection
- Rule loading
- Server communication
- Authorization issues

Logs are your first troubleshooting tool.

---

## Common Scanner Problems

Typical issues include:
- Wrong project key
- Missing permissions
- Unsupported language version
- Scanner and server version mismatch

Most issues are configuration-related, not code-related.

---

## Key Takeaway

The Sonar Scanner is a **data collector**, not a decision maker.

Understanding how it runs and communicates:
- Simplifies CI/CD integration
- Makes troubleshooting easier
- Prevents false assumptions

---

➡️ **Next:** Database & Elasticsearch Internals  
