---
sidebar_position: 7
---

# Network & Ingress Security

Network exposure is one of the **most common Jenkins security failures**.
Many Jenkins instances are compromised simply because they are reachable.

---

## Why Network Security Matters

If Jenkins is reachable:
- Attackers can brute-force logins
- Exploit plugin vulnerabilities
- Abuse APIs
- Pivot into internal systems

Network controls are the **first security boundary**.

---

## Jenkins Exposure Models

### Publicly Exposed Jenkins (High Risk)
- Internet-facing UI
- Requires strict controls
- Strongly discouraged unless necessary

---

### Private Jenkins (Recommended)
- Accessible only via VPN / private network
- Ingress controlled by gateway
- Reduced attack surface

---

## HTTPS Everywhere

Mandatory:
- TLS termination (Ingress / Load Balancer)
- Secure cookies enabled
- HSTS if public

Never expose Jenkins over HTTP.

---

## Ingress Controls

Recommended controls:
- IP allowlists
- Authentication at gateway
- Rate limiting
- Web Application Firewall (WAF)

Ingress should block attacks before Jenkins.

---

## Reverse Proxy Best Practices

Common proxies:
- NGINX
- HAProxy
- Cloud load balancers

Rules:
- Do not expose Jenkins directly
- Forward only required headers
- Limit request sizes

---

## Webhook Ingress Security

- Restrict webhook endpoints
- Validate webhook secrets
- Allow only SCM IP ranges

Webhooks are a frequent attack vector.

---

## API & CLI Exposure

- Disable Jenkins CLI if unused
- Restrict API token usage
- Rate-limit API access

APIs are powerful and dangerous.

---

## Agent Network Segmentation

- Separate controller and agent networks
- Restrict east-west traffic
- Agents should not access internal systems freely

---

## Kubernetes Ingress Security

- Use Ingress controllers
- Apply NetworkPolicies
- Separate namespaces
- Restrict service accounts

---

## Common Network Security Failures

- Public Jenkins without protection
- No IP restrictions
- No HTTPS
- Exposed CLI port

---

## Best Practices

- Private Jenkins by default
- Defense-in-depth at network layer
- Monitor ingress logs
- Regularly review exposure

---

## Interview Focus Areas

- Why Jenkins should not be public
- Role of reverse proxy
- Network vs application security

