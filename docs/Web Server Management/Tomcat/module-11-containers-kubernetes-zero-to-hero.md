---
sidebar_position: 11
title: Containers & Kubernetes
---

# Containers & Kubernetes 

Modern applications are no longer deployed only on virtual machines.

Today, most production systems use containers and orchestration
platforms.

In this module, you will clearly understand:

-   What is a container?
-   How Tomcat runs inside Docker
-   Writing a simple Dockerfile
-   Environment variables in containers
-   Basic container best practices
-   Kubernetes basics (Deployment, Service, Ingress)
-   Liveness and Readiness probes
-   Scaling pods
-   VM-based vs Container-based deployment differences

This module connects Tomcat with modern cloud-native environments.

------------------------------------------------------------------------

# 1. What is a Container?

A container is a lightweight package that includes:

-   Application
-   Dependencies
-   Runtime
-   Configuration

It runs consistently across environments.

Unlike VMs: Containers share the host OS kernel.

Benefits:

-   Fast startup
-   Lightweight
-   Easy scaling
-   Consistent deployments

------------------------------------------------------------------------

# 2. Running Tomcat in Docker

Instead of installing Tomcat manually on server, we can use official
Docker image.

Basic command:

    docker run -d -p 8080:8080 tomcat:9

This means:

-   Pull Tomcat image
-   Run container
-   Map port 8080

Access:

    http://localhost:8080

Now Tomcat runs inside container.

------------------------------------------------------------------------

# 3. Writing a Simple Dockerfile

Example Dockerfile:

FROM tomcat:9-jdk17

COPY app.war /usr/local/tomcat/webapps/

EXPOSE 8080

Build image:

    docker build -t mytomcat-app .

Run:

    docker run -d -p 8080:8080 mytomcat-app

Now your application runs inside container.

------------------------------------------------------------------------

# 4. Environment Variables in Containers

Instead of editing config files manually, use environment variables.

Example:

    docker run -e JAVA_OPTS="-Xms512m -Xmx1024m" ...

Containers should be configured via:

-   Environment variables
-   Config files mounted as volumes

Never hardcode secrets in image.

------------------------------------------------------------------------

# 5. Container Best Practices

✔ Use specific image version (avoid latest)\
✔ Keep image small\
✔ Do not run container as root\
✔ Store logs externally\
✔ Use health checks\
✔ Keep configuration external

Containers should be immutable.

------------------------------------------------------------------------

# 6. What is Kubernetes?

Kubernetes is container orchestration platform.

It manages:

-   Deployment
-   Scaling
-   Networking
-   Self-healing
-   Load balancing

Instead of running one container manually, Kubernetes manages many
automatically.

------------------------------------------------------------------------

# 7. Kubernetes Deployment

A Deployment defines:

-   Number of replicas
-   Container image
-   Resource limits

Example YAML:

apiVersion: apps/v1 kind: Deployment metadata: name: tomcat-app spec:
replicas: 2 template: spec: containers: - name: tomcat image:
mytomcat-app ports: - containerPort: 8080

replicas: 2 means two pods running.

------------------------------------------------------------------------

# 8. Kubernetes Service

Service exposes pods internally or externally.

Types:

ClusterIP → Internal access\
NodePort → Exposes on node port\
LoadBalancer → Cloud load balancer

Service provides stable access to pods.

------------------------------------------------------------------------

# 9. Ingress (Basic Idea)

Ingress manages external HTTP access.

Instead of exposing each service, Ingress routes traffic based on
domain/path.

Example:

myapp.com → Tomcat service

Ingress often handles SSL termination.

------------------------------------------------------------------------

# 10. Liveness and Readiness Probes

Very important concept.

Liveness Probe: Checks if container is alive. If fails → Kubernetes
restarts pod.

Readiness Probe: Checks if app is ready to receive traffic. If fails →
Traffic not sent to pod.

Example:

readinessProbe: httpGet: path: /health port: 8080

Without probes: Traffic may go to unhealthy pod.

------------------------------------------------------------------------

# 11. Scaling Pods

Scaling in Kubernetes is easy.

Increase replicas:

replicas: 3

Now three pods running.

Kubernetes distributes traffic automatically.

Horizontal scaling is default in container world.

------------------------------------------------------------------------

# 12. VM-Based vs Container-Based Deployment

VM-Based:

-   Heavy
-   Slower startup
-   Manual scaling

Container-Based:

-   Lightweight
-   Fast startup
-   Easy scaling
-   Automated healing

Modern production prefers containers.

------------------------------------------------------------------------

# 13. Common Container Mistakes

❌ Using latest tag\
❌ Hardcoding secrets\
❌ No resource limits\
❌ No health checks\
❌ Logging only inside container

Always follow best practices.

------------------------------------------------------------------------

# Summary

After completing this module, you should:

✔ Understand containers clearly\
✔ Run Tomcat inside Docker\
✔ Write simple Dockerfile\
✔ Understand Kubernetes Deployment\
✔ Understand Service & Ingress\
✔ Configure health probes\
✔ Scale pods confidently\
✔ Understand VM vs container differences

Next: Upgrade, Backup & Disaster Recovery
