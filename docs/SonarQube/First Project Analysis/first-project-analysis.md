---
sidebar_position: 9
---

# First Project Analysis – Running Your First Scan

This is the moment where SonarQube stops being theory and starts becoming **real**.
In this chapter, we will walk through analyzing a project for the first time and, more importantly,
**understanding what is actually happening**.

---

## Creating a Project in SonarQube

Before running any scan, SonarQube needs to know **what project it is analyzing**.

When you create a project, SonarQube assigns:
- A **Project Key** (unique identifier)
- A **Display Name**
- A **Default Quality Gate**

The project key is critical — it is how the scanner maps analysis results to the correct project.

---

## Understanding Project Keys

A Project Key:
- Must be unique in SonarQube
- Is usually based on repository or application name
- Should remain stable over time

Changing the project key later creates a **new project**, not an update.

---

## Generating an Authentication Token

SonarQube uses **tokens**, not usernames/passwords, for scans.

Tokens:
- Represent machine access
- Are tied to user permissions
- Can be revoked anytime

Best practice:
- Create one token per CI pipeline
- Store it securely in CI secret storage

---

## Preparing the Project for Scanning

Before running the scanner, ensure:
- Source code is present
- Language versions are supported
- Tests and coverage reports are generated (if applicable)

SonarQube analyzes what it sees — missing inputs lead to incomplete results.

---

## Running the First Scan

A basic scan usually involves:
- Providing project key
- Providing server URL
- Providing authentication token

When the scan starts, the scanner will:
- Detect languages
- Load rules
- Analyze files
- Send results to the server

A successful scan means data was **sent**, not yet approved.

---

## Understanding Scanner Output

Scanner logs provide important clues:
- Which files were analyzed
- Which languages were detected
- Whether rules were applied correctly
- Whether results were uploaded successfully

Always review logs if results look unexpected.

---

## Viewing Results in the UI

After the scan:
- Open the project dashboard
- Review issues and metrics
- Check Quality Gate status

Do not try to fix everything immediately.
Focus on **high-impact issues first**.

---

## Common Beginner Mistakes

Avoid these common issues:
- Using the wrong project key
- Forgetting authentication tokens
- Scanning compiled or generated files
- Ignoring scanner warnings

Most first-scan problems are configuration-related.

---

## Key Takeaway

Your first scan sets the foundation for everything that follows.

A clean, well-understood first analysis:
- Builds confidence
- Makes future scans predictable
- Prevents confusion later

---

➡️ **Next:** Understanding Analysis Results  
