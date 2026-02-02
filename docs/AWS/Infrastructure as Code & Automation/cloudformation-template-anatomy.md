---
sidebar_position: 3
title: CloudFormation Template Anatomy
---

# CloudFormation Template Anatomy

Understanding the **structure of a CloudFormation template** is essential before writing real infrastructure code.
This document walks through **each template section**, explains its purpose, and shows how they fit together.

---

## Template Format

CloudFormation templates are written in:
- YAML (recommended)
- JSON

YAML is preferred because:
- More readable
- Less verbose

---

## Basic Template Skeleton

```yaml
AWSTemplateFormatVersion: '2010-09-09'
Description: Sample CloudFormation template

Parameters:
  ...

Resources:
  ...

Outputs:
  ...
```

This is the **minimum mental model**.

---

## AWSTemplateFormatVersion

- Specifies template format version
- Always use: `2010-09-09`

This value:
- Does not change
- Is required for clarity

---

## Description

- Human-readable description
- Explains what the stack creates

Best practice:
- Keep it short and meaningful

---

## Parameters Section

Parameters:
- Accept runtime input
- Make templates reusable

Example:
```yaml
Parameters:
  InstanceType:
    Type: String
    Default: t3.micro
```

Avoid:
- Hardcoding environment-specific values

---

## Resources Section (Most Important)

Resources define:
- Actual AWS resources to be created

Example:
```yaml
Resources:
  MyEC2Instance:
    Type: AWS::EC2::Instance
    Properties:
      InstanceType: !Ref InstanceType
```

Every template **must have Resources**.

---

## Intrinsic Functions (Preview)

CloudFormation provides built-in functions:
- !Ref
- !GetAtt
- !Sub
- !Join

These enable:
- Dynamic values
- Cross-resource references

We will cover these in detail next.

---

## Mappings

Mappings:
- Static lookup tables

Use cases:
- Region-based AMIs
- Environment-based values

Example:
```yaml
Mappings:
  RegionMap:
    us-east-1:
      AMI: ami-123
```

---

## Conditions

Conditions:
- Control resource creation
- Enable environment-specific logic

Example:
```yaml
Conditions:
  IsProd: !Equals [ !Ref EnvType, prod ]
```

---

## Outputs Section

Outputs:
- Export useful values
- Share values across stacks

Example:
```yaml
Outputs:
  InstanceId:
    Value: !Ref MyEC2Instance
```

---

## Metadata (Optional)

Metadata:
- Used by tools
- Includes UI hints

Rarely required for beginners.

---

## Template Execution Flow

High-level flow:
1. Parameters evaluated
2. Conditions resolved
3. Resources created
4. Outputs generated

Understanding flow prevents surprises.

---

## Common Beginner Mistakes

- Huge single template
- No parameters
- Hardcoded values
- Ignoring conditions

These reduce reusability.

---

## Interview Tip

If asked:
> “What are the main sections of a CloudFormation template?”

Strong answer:
> Parameters, Resources, and Outputs, with optional sections like Mappings and Conditions.

---

## Key Takeaways

- Templates are declarative
- Resources are the core section
- Parameters increase reusability
- Outputs enable integration
- Structure matters

---

📌 **Next:** CloudFormation Intrinsic Functions Deep Dive
