---
sidebar_position: 3
---

# Quality Profiles – Defining the Rules

After understanding how SonarQube thinks about code quality, the next logical step is to understand
**how SonarQube decides what is right and what is wrong**.

That decision is driven by **Quality Profiles**.

---

## What Is a Quality Profile?

A Quality Profile is simply a **set of rules** that SonarQube uses when analyzing code.

You can think of it as:
> “The rulebook SonarQube follows while reviewing your code.”

Each programming language in SonarQube has its **own Quality Profile**.

---

## Why Quality Profiles Exist

Different teams and projects have different needs.

For example:
- A banking application needs stricter security rules
- A prototype project may prioritize speed over perfection
- Legacy systems cannot fix everything at once

Quality Profiles allow teams to:
- Enforce standards consistently
- Adapt rules to real-world constraints
- Improve quality gradually instead of blocking development

---

## Default Quality Profiles

SonarQube provides **default Quality Profiles** out of the box.

These profiles:
- Are created and maintained by SonarSource
- Represent industry best practices
- Are safe starting points for most teams

For beginners and new projects, using the default profile is strongly recommended.

---

## Custom Quality Profiles

As teams mature, they often need custom rules.

Custom Quality Profiles allow you to:
- Enable or disable specific rules
- Adjust rule severity
- Align rules with company standards

A common strategy is:
1. Start with the default profile
2. Copy it
3. Modify rules gradually

This avoids overwhelming developers.

---

## Rule Activation and Severity

Each rule in a Quality Profile has:
- A purpose
- A severity level (Minor, Major, Critical, Blocker)

Severity helps teams prioritize:
- Blocker & Critical → Must fix
- Major → Fix soon
- Minor → Improve when possible

Changing severity does **not** change detection logic, only importance.

---

## One Profile Per Language

Important rule:
> A Quality Profile applies **per language**, not per project.

For example:
- Java code uses a Java profile
- JavaScript code uses a JavaScript profile

A single project may use **multiple profiles** if it contains multiple languages.

---

## Assigning Quality Profiles to Projects

Projects automatically inherit:
- The default profile for each language

Admins can:
- Assign a custom profile
- Change profiles without rescanning code

This flexibility helps during migrations and audits.

---

## Common Mistakes with Quality Profiles

Avoid these beginner mistakes:

- Creating too many profiles
- Enabling every rule blindly
- Making rules too strict early
- Changing profiles without team communication

Quality Profiles should **guide**, not punish.

---

## Best Practice Strategy

A proven approach:
- Start simple
- Focus on new code
- Tighten rules gradually
- Review impact regularly

This builds trust between developers and the platform.

---

## Key Takeaway

Quality Profiles define **how strict SonarQube is** when reviewing code.

Well-designed profiles:
- Improve quality
- Reduce friction
- Support long-term maintainability

---

➡️ **Next:** Quality Gates – Pass or Fail Decisions  
