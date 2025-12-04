---
sidebar_position: 2
---

# Kubernetes Basics

---

## 1. What is Kubernetes?

### Definition
Kubernetes (often abbreviated as **K8s**) is an **open-source container orchestration platform** used to automate the **deployment, scaling, management, and self-healing** of containerized applications.

### Simple Explanation
> Kubernetes is a system that manages containers automatically so applications run reliably in production.

### Technical Explanation
Kubernetes is a **distributed control system** that continuously ensures the **actual state** of applications matches the **desired state** defined by users using declarative YAML files.

---

## 2. Why Do We Need Kubernetes?

Modern applications are:
- Built using microservices
- Deployed using containers (Docker)
- Expected to scale automatically
- Required to be always available

Without Kubernetes:
- Manual deployment and scaling
- Downtime during failures
- Complex container networking
- Difficult upgrades and rollbacks

With Kubernetes:
✅ Automated operations  
✅ High availability  
✅ Scalability  
✅ Infrastructure independence  

---

## 3. Problems Kubernetes Solves

---

### 3.1 Scaling Problem

#### Without Kubernetes
- Applications need to be scaled manually
- Over-provisioning wastes resources
- Under-provisioning causes downtime

#### With Kubernetes
Kubernetes provides **horizontal scaling**, where the number of application instances (Pods) can increase or decrease automatically based on load.

✅ Features involved:
- Horizontal Pod Autoscaler (HPA)
- ReplicaSets
- Deployments

**Conceptual View**
```
High Traffic  -> More Pods
Low Traffic   -> Fewer Pods
```

---

### 3.2 Self-Healing Problem

#### Without Kubernetes
- Application crashes require manual restart
- Node failures cause long outages

#### With Kubernetes
Kubernetes continuously monitors application health and takes automated corrective action:

- Restarts failed containers
- Recreates failed Pods
- Replaces unhealthy Nodes
- Ensures correct replica count

✅ Features involved:
- Health checks
- Restart policies
- Controllers

**Self-Healing Flow**
```
Pod Fails -> Controller Detects -> New Pod Created
```

---

### 3.3 Orchestration Problem

#### What is Orchestration?
Orchestration means **coordinating multiple containers** so they function together as a single application.

#### Without Kubernetes
- Manual container startup order
- Complex networking
- No built-in load balancing

#### With Kubernetes
Kubernetes automatically orchestrates:
- Container scheduling
- Networking & service discovery
- Load balancing
- Configuration & secret management
- Rolling updates and rollbacks

✅ Result:
> Containers work together seamlessly without manual intervention.

---

## 4. Kubernetes vs Docker Swarm

| Feature | Kubernetes | Docker Swarm |
|------|------------|--------------|
| Learning curve | Steep | Easy |
| Scalability | Very High | Limited |
| Self-healing | Advanced | Basic |
| Auto-scaling | Yes | Limited |
| Ecosystem | Very Large | Small |
| Production Adoption | Industry Standard | Declining |

### Summary
- Docker Swarm is simple and easy to learn
- Kubernetes is complex but extremely powerful
- Kubernetes is the preferred choice for production systems

---

## 5. Kubernetes Architecture Overview

Kubernetes follows a **Control Plane + Worker Node** architecture.

---

### 5.1 High-Level Architecture

```
+---------------------+
|   Control Plane     |
+---------------------+
           |
           |
+---------------------+
|   Worker Nodes      |
+---------------------+
```

---

![alt text](../Images/Architecture.png)