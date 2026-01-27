---
sidebar_position: 7
title: Load Balancers in AWS
---

# Load Balancers in AWS (ALB, NLB, CLB)

Load Balancers are the **traffic managers** of AWS.
They sit in front of your application and decide **which server should handle each request**.

Without load balancers:
- One server handles all traffic
- A single failure causes downtime
- Scaling becomes manual and risky

With load balancers:
- Traffic is distributed automatically
- Applications stay available
- Scaling becomes seamless

---

## Why Load Balancers Are Critical

In real-world systems:
- Traffic is unpredictable
- Servers fail
- Applications must stay online

Load balancers solve these problems by:
- Distributing traffic
- Performing health checks
- Working with Auto Scaling Groups

👉 Load balancers are **mandatory for production workloads**.

---

## Types of AWS Load Balancers

AWS provides **three main types** of load balancers:

1. Application Load Balancer (ALB)  
2. Network Load Balancer (NLB)  
3. Classic Load Balancer (CLB – legacy)

Each is designed for **different use cases**.

---

## 🌐 Application Load Balancer (ALB)

### What ALB Is Best At
- HTTP and HTTPS traffic
- Layer 7 (application layer) routing

### Key Features
- Path-based routing (`/api`, `/images`)
- Host-based routing (`api.example.com`)
- SSL termination
- WebSocket support

### Common Use Cases
- Web applications
- Microservices
- REST APIs
- Container workloads (ECS/EKS)

👉 **ALB is the most commonly used load balancer today.**

---

## ⚡ Network Load Balancer (NLB)

### What NLB Is Best At
- Extremely high performance
- Layer 4 (TCP/UDP) traffic

### Key Features
- Ultra-low latency
- Static IP addresses
- Handles millions of requests per second

### Common Use Cases
- High-performance applications
- TCP-based services
- Gaming servers
- Real-time systems

👉 Choose NLB when **performance and latency matter most**.

---

## 🕰️ Classic Load Balancer (CLB)

### What CLB Is
- Legacy load balancer
- Supports basic Layer 4 and Layer 7

### Important Note
AWS recommends:
- Use ALB or NLB for new workloads
- Avoid CLB unless maintaining legacy systems

👉 CLB exists mainly for backward compatibility.

---

## ALB vs NLB vs CLB (Quick Comparison)

| Feature | ALB | NLB | CLB |
|------|-----|-----|-----|
| OSI Layer | Layer 7 | Layer 4 | Layer 4 & 7 |
| Protocols | HTTP/HTTPS | TCP/UDP | HTTP/TCP |
| Routing | Advanced | Basic | Limited |
| Performance | High | Very High | Medium |
| Use Today | Yes | Yes | Rare |

---

## Load Balancers with Auto Scaling

Typical production flow:
1. User sends request
2. Load Balancer receives traffic
3. Traffic sent to healthy EC2 instances
4. ASG adds/removes instances as needed

This setup provides:
- High availability
- Fault tolerance
- Horizontal scalability

---

## Common Beginner Mistakes

- Using CLB for new applications
- Not enabling health checks
- Putting instances in only one AZ
- Exposing EC2 directly to the internet

👉 Always expose **Load Balancer**, not EC2.

---

## Interview Tip

If asked:
> “Which load balancer should I use?”

Strong answer:
> Use ALB for HTTP/HTTPS applications, NLB for high-performance TCP/UDP workloads, and avoid CLB for new systems.

This shows **clear AWS decision-making**.

---

## Key Takeaways

- Load balancers distribute traffic
- ALB is best for web apps
- NLB is best for performance
- CLB is legacy
- Core component of scalable architectures

---

📌 **Next:** Launch Templates and Launch Configurations
