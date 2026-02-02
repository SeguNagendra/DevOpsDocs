---
sidebar_position: 12
---

# SonarQube with Jenkins – End-to-End Pipeline Integration

Jenkins is one of the most common CI tools used with SonarQube.
Understanding this integration clearly helps you apply the same concepts to other CI systems as well.

This chapter explains **how SonarQube fits into a Jenkins pipeline**, step by step.

---

## Why Jenkins + SonarQube Is So Common

Many organizations use Jenkins because:
- It is flexible and extensible
- It integrates with almost any tool
- It supports complex pipelines

SonarQube fits naturally into Jenkins pipelines as a **quality control stage**.

---

## Integration Approaches

There are two main ways to integrate SonarQube with Jenkins.

### Jenkins SonarQube Plugin
- Simplifies configuration
- Provides built-in Quality Gate checks
- Recommended for most teams

### CLI-Based Integration
- Uses sonar-scanner directly
- More control, more configuration
- Useful in custom setups

For beginners and most enterprises, the plugin approach is preferred.

---

## Prerequisites

Before integration, ensure:
- SonarQube server is reachable from Jenkins
- SonarQube plugin is installed in Jenkins
- Authentication token is created in SonarQube
- Jenkins credentials are configured securely

Skipping prerequisites causes most integration failures.

---

## Typical Jenkins Pipeline Flow

A standard pipeline usually follows this order:

1. Checkout code
2. Build and run tests
3. Run SonarQube analysis
4. Wait for Quality Gate result
5. Pass or fail the pipeline

SonarQube should run **after tests**, not before.

---

## Quality Gate Enforcement

Jenkins can:
- Pause the pipeline
- Fetch Quality Gate status from SonarQube
- Fail the build if the gate fails

This ensures:
- Bad code never gets deployed
- Developers receive immediate feedback

Quality Gates are what make SonarQube actionable.

---

## Declarative Pipeline Example (Conceptual)

In declarative pipelines:
- SonarQube runs as a stage
- Quality Gate is checked explicitly
- Failures stop further stages

The exact syntax varies, but the concept remains the same.

---

## Common Jenkins + SonarQube Issues

Frequently seen problems:
- Jenkins cannot reach SonarQube server
- Quality Gate status never returns
- Token permission issues
- Scanner and server version mismatch

Most issues are configuration-related, not tool bugs.

---

## Best Practices

Follow these guidelines:
- Use environment variables for configuration
- Store tokens in Jenkins credentials
- Fail fast on Quality Gate failure
- Monitor scan duration

These practices improve reliability and trust.

---

## Key Takeaway

Jenkins + SonarQube integration turns code quality into an **automated gate**, not a manual check.

Once teams experience this flow, manual quality checks feel outdated.

---

➡️ **Next:** SonarQube with GitHub / GitLab  
