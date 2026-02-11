---
sidebar_position: 10
title: Containers & Kubernetes Integration 
---

# Containers & Kubernetes Integration

Modern infrastructure is container-first.

NGINX is widely used:

-   As a Docker container
-   As a sidecar proxy
-   As Kubernetes Ingress Controller
-   As edge gateway in cloud-native systems

In this module, we cover:

-   Running NGINX in Docker
-   Writing clean Dockerfile
-   Environment-based configuration
-   NGINX in Kubernetes
-   ConfigMaps
-   Ingress basics
-   Liveness & Readiness probes
-   Scaling pods
-   Architect-level cloud-native thinking

Layered format:

🟢 Beginner\
🔵 DevOps Practical\
🔴 Architect Insight\
⚫ Real Production Scenario

------------------------------------------------------------------------

## 1. Running NGINX in Docker

### 🟢 Beginner Understanding

Instead of installing NGINX on VM, you can run it inside a container.

Example:

docker run -d -p 80:80 nginx

This pulls official NGINX image and starts container.

------------------------------------------------------------------------

### 🔵 DevOps Practical View

Custom configuration:

docker run -d -p 80:80 -v /my/nginx.conf:/etc/nginx/nginx.conf nginx

Mount configuration file into container.

------------------------------------------------------------------------

### 🔴 Architect-Level Insight

Containers provide:

-   Consistent runtime
-   Faster scaling
-   Immutable infrastructure

But containerized NGINX still depends on:

-   Host kernel limits
-   File descriptors
-   Network stack performance

------------------------------------------------------------------------

### ⚫ Real Production Scenario

Migrated VM-based NGINX to Docker.

Deployment became reproducible across environments.

------------------------------------------------------------------------

## 2. Writing a Clean Dockerfile

### 🟢 Beginner Understanding

You can build custom image with your config.

Example:

FROM nginx:1.25 COPY nginx.conf /etc/nginx/nginx.conf

------------------------------------------------------------------------

### 🔵 DevOps Practical View

Best practices:

-   Use specific version tag (not latest)
-   Avoid modifying container manually
-   Keep image small
-   Externalize configuration

------------------------------------------------------------------------

### 🔴 Architect-Level Insight

Image should be immutable.

Configuration should be:

-   Environment-driven
-   Or mounted via volumes
-   Or injected via orchestration layer

Separation of image and configuration improves scalability.

------------------------------------------------------------------------

### ⚫ Real Production Scenario

Production container failed after rebuild because "latest" tag changed
upstream behavior.

Pinned version solved issue.

------------------------------------------------------------------------

# 3. Environment-Based Configuration

## 🟢 Beginner Understanding

Different environments need different configs.

Dev, QA, Prod should not share same settings.

------------------------------------------------------------------------

## 🔵 DevOps Practical View

Use:

-   Environment variables
-   Separate config files
-   Templates (envsubst)

Example:

envsubst \< template.conf \> nginx.conf

------------------------------------------------------------------------

## 🔴 Architect-Level Insight

In cloud-native systems:

Configuration must be dynamic.

Never hardcode:

-   Backend IPs
-   Secrets
-   Environment-specific values

------------------------------------------------------------------------

## ⚫ Real Production Scenario

Production outage occurred because QA backend IP was hardcoded in image.

------------------------------------------------------------------------

# 4. NGINX in Kubernetes

## 🟢 Beginner Understanding

Kubernetes runs containers in pods.

NGINX runs as a pod.

------------------------------------------------------------------------

## 🔵 DevOps Practical View

Example Deployment:

apiVersion: apps/v1 kind: Deployment spec: replicas: 2 template: spec:
containers: - name: nginx image: nginx:1.25

------------------------------------------------------------------------

## 🔴 Architect-Level Insight

Kubernetes manages:

-   Scaling
-   Self-healing
-   Service discovery

NGINX inside Kubernetes must be designed stateless.

------------------------------------------------------------------------

## ⚫ Real Production Scenario

Pod crashed.

Kubernetes automatically restarted it.

No manual intervention required.

------------------------------------------------------------------------

# 5. ConfigMaps

## 🟢 Beginner Understanding

ConfigMap stores configuration outside container image.

------------------------------------------------------------------------

## 🔵 DevOps Practical View

Mount config into pod:

volumeMounts: - name: nginx-config mountPath: /etc/nginx/nginx.conf

------------------------------------------------------------------------

## 🔴 Architect-Level Insight

Separating config from image allows:

-   Rolling updates
-   Environment-specific configuration
-   Dynamic changes

Configuration becomes first-class object.

------------------------------------------------------------------------

## ⚫ Real Production Scenario

Needed urgent routing change.

Updated ConfigMap and reloaded pods without rebuilding image.

------------------------------------------------------------------------

# 6. Ingress Controller Basics

## 🟢 Beginner Understanding

Ingress exposes services externally in Kubernetes.

NGINX is commonly used as Ingress controller.

------------------------------------------------------------------------

## 🔵 DevOps Practical View

Ingress example:

apiVersion: networking.k8s.io/v1 kind: Ingress spec: rules: - host:
app.example.com http: paths: - path: / backend: service: name:
app-service

------------------------------------------------------------------------

## 🔴 Architect-Level Insight

Ingress controller handles:

-   Routing
-   SSL termination
-   Path-based routing
-   Load balancing

It becomes edge gateway of cluster.

------------------------------------------------------------------------

## ⚫ Real Production Scenario

Multiple microservices exposed through single NGINX Ingress.

Simplified external access management.

------------------------------------------------------------------------

# 7. Liveness & Readiness Probes

## 🟢 Beginner Understanding

Kubernetes checks if container is alive and ready.

------------------------------------------------------------------------

## 🔵 DevOps Practical View

Example:

readinessProbe: httpGet: path: /health port: 80

If probe fails, traffic is not sent to pod.

------------------------------------------------------------------------

## 🔴 Architect-Level Insight

Readiness protects users from:

-   Cold starts
-   Partially initialized services

Liveness prevents zombie containers.

------------------------------------------------------------------------

## ⚫ Real Production Scenario

Deployment caused brief outage because readiness probe was missing.

Traffic routed to pod before it was ready.

------------------------------------------------------------------------

# 8. Scaling Pods

## 🟢 Beginner Understanding

Increase replicas to handle more traffic.

------------------------------------------------------------------------

## 🔵 DevOps Practical View

Change:

replicas: 2 → replicas: 5

Kubernetes distributes traffic automatically.

------------------------------------------------------------------------

## 🔴 Architect-Level Insight

Horizontal scaling requires:

-   Stateless design
-   Shared session store (if needed)
-   Externalized state

NGINX scales well horizontally.

------------------------------------------------------------------------

## ⚫ Real Production Scenario

Traffic doubled during campaign.

Increased replicas from 3 to 8. System handled load without downtime.

------------------------------------------------------------------------

# Summary

After this module, you understand:

✔ Running NGINX in Docker\
✔ Writing clean Dockerfile\
✔ Environment-based configuration\
✔ NGINX in Kubernetes\
✔ ConfigMaps usage\
✔ Ingress basics\
✔ Health probes\
✔ Scaling strategy\
✔ Cloud-native architectural thinking

Next: Real-World Incidents & Interview Preparation (Layered).
