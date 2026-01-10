
# AWS IAM – Complete Notes (DevOps & Cloud Architect Perspective)

## What is AWS IAM?
AWS Identity and Access Management (IAM) is a global AWS service used to securely control access to AWS resources.

IAM answers three questions:
- Who are you? (User / Role)
- What can you do? (Policy)
- On which resource? (ARN)

IAM = Authentication + Authorization

---

## Why IAM is Important (Real-World)
Without IAM:
- Any user can delete production resources
- AWS credentials may leak
- No audit trail

With IAM:
- Least privilege access
- Secure automation
- Compliance-ready (ISO, SOC, HIPAA)

---

## IAM Core Components
- Users
- Groups
- Policies
- Roles
- Identity Providers

---

## IAM Users
IAM Users represent humans or service accounts.

Best Practices:
- Never use root user for daily work
- Enable MFA
- Rotate access keys
- Avoid long-lived users

Real Example:
A developer needs only EC2 read and S3 upload access – not admin.

---

## IAM Groups
Groups simplify permission management.

Example:
- Dev Group → EC2 Read
- QA Group → Read Only
- DevOps Group → Full Infra

Users inherit permissions from groups.

---

## IAM Policies (Most Important)
Policies are JSON documents defining permissions.

### EC2 Read Only Policy
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "ec2:Describe*",
      "Resource": "*"
    }
  ]
}
```

### S3 Upload Only Policy
```json
{
  "Effect": "Allow",
  "Action": "s3:PutObject",
  "Resource": "arn:aws:s3:::dev-bucket/*"
}
```

Policy Evaluation:
1. Explicit Deny
2. Explicit Allow
3. Default Deny

---

## Managed vs Inline Policies
- AWS Managed – Generic
- Customer Managed – Best Practice
- Inline – Avoid in production

---

## IAM Roles (DevOps Core)
Roles provide temporary access without credentials.

Used by:
- EC2
- Lambda
- EKS
- CI/CD tools

### EC2 to S3 Access Role Policy
```json
{
  "Effect": "Allow",
  "Action": [
    "s3:GetObject",
    "s3:PutObject"
  ],
  "Resource": "arn:aws:s3:::logs-bucket/*"
}
```

---

## Trust Policy
Defines who can assume the role.

Example: EC2 Trust Policy
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "Service": "ec2.amazonaws.com"
      },
      "Action": "sts:AssumeRole"
    }
  ]
}
```

---

## Cross-Account Access
Used when accessing prod from dev account.

Benefits:
- No shared credentials
- Secure delegation
- Easy revocation

---

## IAM with CI/CD
Modern approach:
- Use OIDC with IAM roles
- Avoid storing AWS keys

Benefits:
- Temporary credentials
- No secrets
- Least privilege

---

## Security Best Practices
- Enable MFA on root
- Disable root access keys
- Use roles instead of users
- Enable CloudTrail
- Rotate keys regularly

---

## Common Mistakes
- Admin access to everyone
- Hardcoded credentials
- No MFA
- Inline policies in prod

---

## Interview Quick Notes
- User vs Role → Permanent vs Temporary
- Default IAM behavior → Deny
- Most secure access → Role + OIDC
- Auditing → CloudTrail

---

## Final Advice
IAM is the foundation of AWS security.
Weak IAM = Compromised cloud.
Strong IAM = Scalable and secure architecture.
