---
sidebar_position: 10
title: DevOps & Automation Integration
---

# DevOps & Automation Integration

So far, you have learned:

-   How Tomcat works
-   How to configure it
-   How to secure it
-   How to scale it

Now we move into real DevOps territory.

In modern environments:

❌ We do NOT manually copy WAR files in production.\
❌ We do NOT SSH into server for every deployment.

We use automation.

In this module, you will clearly understand:

-   What CI/CD means
-   How deployment pipeline works
-   How Tomcat fits into CI/CD
-   Artifact management basics
-   Environment-based configuration
-   Secrets handling basics
-   Zero-downtime deployment practical view

------------------------------------------------------------------------

# 1. What is CI/CD?

CI = Continuous Integration\
CD = Continuous Delivery / Deployment

CI means:

-   Developers push code
-   Code is built automatically
-   Tests run automatically
-   WAR file generated automatically

CD means:

-   WAR file deployed automatically
-   No manual steps
-   Repeatable and reliable process

This reduces human errors.

------------------------------------------------------------------------

# 2. Basic CI/CD Flow with Tomcat

Typical flow:

1.  Developer pushes code to Git repository.
2.  CI tool (like Jenkins) pulls code.
3.  Build tool (Maven/Gradle) builds WAR file.
4.  WAR stored in artifact repository.
5.  Deployment stage pushes WAR to Tomcat.
6.  Tomcat reloads application.

This is automated pipeline.

------------------------------------------------------------------------

# 3. Deployment Strategies in DevOps

Manual Deployment (Old Way): - SSH - Copy WAR - Restart Tomcat

Automated Deployment (Modern Way): - Pipeline handles deployment -
Health check before marking success - Rollback supported

Automation reduces downtime risk.

------------------------------------------------------------------------

# 4. Artifact Management Basics

After build, WAR file should not be lost.

It should be stored in:

-   Artifact repository (Nexus, Artifactory)
-   Versioned storage

Why?

If new version fails, you can redeploy older stable version.

Artifact versioning is critical in production.

------------------------------------------------------------------------

# 5. Environment-Based Configuration

Dev, QA, and Prod should NOT use same configuration.

Avoid hardcoding:

-   Database credentials
-   URLs
-   API keys

Better approach:

-   Use external property files
-   Use environment variables
-   Use JNDI configuration

Example:

Instead of hardcoding DB URL in code, define in context.xml or
environment file.

This allows same WAR to run in all environments.

------------------------------------------------------------------------

# 6. Secrets Handling Basics

Never store passwords in:

-   Git repository
-   Plain text inside WAR
-   Public config files

Use:

-   Environment variables
-   Secret managers
-   Encrypted configuration tools

DevOps responsibility is to protect sensitive data.

------------------------------------------------------------------------

# 7. Zero-Downtime Deployment (Practical View)

For production:

Never restart only Tomcat instance.

Basic approach:

-   Two Tomcat instances behind Load Balancer.
-   Remove Instance A from LB.
-   Deploy new version to A.
-   Health check.
-   Add A back.
-   Repeat for B.

This prevents user-facing downtime.

------------------------------------------------------------------------

# 8. Basic Rollback Strategy

If new version fails:

-   Redeploy previous WAR version
-   Or restore previous artifact

Pipeline should allow version selection.

Always keep at least one stable version available.

------------------------------------------------------------------------

# 9. Infrastructure as Code (Basic Idea)

Instead of manually installing Tomcat on servers:

Use automation tools to:

-   Install Java
-   Install Tomcat
-   Configure server.xml
-   Create service
-   Set permissions

This ensures consistent environments.

Manual setup causes configuration drift.

------------------------------------------------------------------------

# 10. Common DevOps Mistakes with Tomcat

❌ Deploying directly to production without testing\
❌ No rollback plan\
❌ Hardcoded configuration\
❌ Exposing management endpoints\
❌ No monitoring after deployment

Automation must include:

-   Logging
-   Health checks
-   Alerts

------------------------------------------------------------------------

# 11. Real-World Deployment Debug Scenario

Scenario: Deployment successful but app not accessible.

Check:

1.  WAR deployed correctly?
2.  Context path correct?
3.  Logs show error?
4.  DB credentials correct?
5.  Load balancer health check passing?

Never assume deployment is perfect. Always verify.

------------------------------------------------------------------------

# Summary

After completing this module, you should:

✔ Understand CI/CD concept\
✔ Know how Tomcat fits into pipeline\
✔ Understand artifact management\
✔ Use environment-based configuration\
✔ Handle secrets safely\
✔ Perform zero-downtime deployment (basic level)\
✔ Understand rollback strategy

Next: Containers & Kubernetes
