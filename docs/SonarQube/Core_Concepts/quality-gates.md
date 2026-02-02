---
sidebar_position: 4
---

# Quality Gates – Pass or Fail Decisions

Quality Profiles define **what rules are checked**.  
Quality Gates decide **whether the code is good enough to move forward**.

This is where SonarQube becomes a **decision-making tool**, not just a reporting tool.

---

## What Is a Quality Gate?

A Quality Gate is a **set of conditions** that code must meet to be considered acceptable.

You can think of it as:
> “The final approval checklist before code is merged or deployed.”

If the code fails the Quality Gate:
- The pipeline can fail
- The pull request can be blocked
- The team must review and fix issues

---

## Why Quality Gates Are Important

Without Quality Gates:
- Issues are visible but ignored
- Bad code slowly enters the codebase
- Quality reports become dashboards nobody checks

With Quality Gates:
- Quality becomes **enforced**, not optional
- Problems are caught early
- Teams build discipline around clean code

---

## Common Quality Gate Conditions

Typical Quality Gate checks include:

- No new bugs
- No new vulnerabilities
- No new security hotspots (or all reviewed)
- Minimum test coverage on new code
- Limited code duplication

These conditions focus on **risk**, not perfection.

---

## New Code vs Overall Code (Critical Concept)

One of SonarQube’s most important ideas is **New Code**.

Why this matters:
- Most projects already contain legacy issues
- Blocking builds because of old problems is unrealistic
- Teams should not introduce *new* problems

Quality Gates usually apply to:
- Code added or changed recently
- New branches and pull requests

This enables **gradual improvement**.

---

## How Quality Gates Work in CI/CD

In CI/CD pipelines:
1. Code is built
2. SonarQube analysis runs
3. Quality Gate status is checked
4. Pipeline continues or fails

This makes quality a **first-class citizen** in the delivery process.

---

## Default vs Custom Quality Gates

SonarQube provides a default Quality Gate that works for most teams.

As organizations mature, they often:
- Create stricter gates
- Use different gates for different projects
- Adjust conditions based on risk level

Best practice:
- Start with the default gate
- Customize only when needed

---

## Common Mistakes with Quality Gates

Avoid these pitfalls:

- Making gates too strict too early
- Applying gates to all legacy code
- Blocking developers without guidance
- Ignoring failed gates

Quality Gates should **guide behavior**, not create frustration.

---

## Designing a Practical Quality Gate

A healthy Quality Gate:
- Focuses on new code
- Prioritizes bugs and vulnerabilities
- Uses realistic coverage thresholds
- Evolves as the team matures

This balances quality and delivery speed.

---

## Key Takeaway

Quality Gates turn SonarQube from a **reporting tool** into a **quality enforcer**.

Well-designed gates:
- Protect the codebase
- Improve developer habits
- Support long-term maintainability

---

➡️ **Next:** Architecture Overview – How SonarQube Works Internally  
