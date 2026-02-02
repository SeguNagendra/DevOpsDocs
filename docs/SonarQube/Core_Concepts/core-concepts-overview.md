---
sidebar_position: 2
---

# Core Concepts – How SonarQube Thinks

Now that we understand **why SonarQube exists**, the next step is to understand **how it thinks**.
This chapter explains the core concepts SonarQube uses to judge code quality.

If you understand this section well, the rest of SonarQube becomes much easier.

---

## How SonarQube Looks at Your Code

SonarQube does not look at code the same way developers do.

Instead of asking:
> “Does this code work?”

SonarQube asks:
> “Is this code safe, reliable, and maintainable over time?”

To answer this, SonarQube categorizes problems into different issue types.

---

## Bugs – Reliability Problems

Bugs are issues that are **likely to cause runtime failures**.

Examples:
- Null pointer dereference
- Incorrect loop conditions
- Resource leaks

These issues may not fail immediately, but they increase the risk of production incidents.

SonarQube treats bugs as **high priority** because they affect application stability.

---

## Vulnerabilities – Security Risks

Vulnerabilities represent **real security threats**.

Examples:
- SQL injection risks
- Hardcoded credentials
- Unsafe deserialization

These issues can be exploited by attackers.
That is why vulnerabilities are treated more seriously than general code smells.

---

## Code Smells – Maintainability Problems

Code smells do not break applications today.

Instead, they:
- Make code harder to understand
- Increase future change risk
- Slow down development over time

Examples:
- Duplicated code
- Overly complex methods
- Poor naming

Ignoring code smells leads to **technical debt**.

---

## Security Hotspots – Needs Human Review

Security hotspots are **sensitive code areas**.

SonarQube cannot decide automatically whether they are safe or unsafe.

Examples:
- Cryptography usage
- Authentication logic
- Access control decisions

These issues require **manual review** by developers or security teams.

---

## Technical Debt – The Hidden Cost

Technical debt represents the **estimated effort required to fix issues**.

SonarQube:
- Calculates remediation effort
- Converts it into technical debt
- Helps teams prioritize cleanup

Managing technical debt prevents systems from becoming unmaintainable.

---

## New Code vs Overall Code (Very Important)

SonarQube focuses heavily on **new code**.

Why?
- Most projects already have legacy issues
- Blocking builds because of old code is unrealistic
- Teams should not add *new* problems

This approach allows gradual improvement without slowing teams down.

---

## Key Takeaway

SonarQube is not judging developers.
It is helping teams **make better decisions about code quality**.

Understanding these core concepts is the foundation for using SonarQube effectively.

---

➡️ **Next:** Quality Profiles – Defining the Rules  
