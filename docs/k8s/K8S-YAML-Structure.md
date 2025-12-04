---
sidebar_position: 6
---

# Kubernetes YAML Structure 

This document explains **YAML fundamentals**, **Kubernetes manifest structure**, and
includes **hands-on labs** such as deploying NGINX, exposing it as a Service, and scaling replicas.

It also sets the base for the **Intermediate Level (Core Workloads & Networking)** topics.

---

# 1. YAML Fundamentals

YAML stands for **YAML Ain’t Markup Language**.

It is:
- Human-readable
- Indentation-based
- Used by Kubernetes to define **desired state**

### Basic YAML Rules
- Use **spaces, not tabs**
- Key-value structure:
```yaml
key: value
```
- Lists:
```yaml
fruits:
  - apple
  - banana
```
- Nesting is done by indentation:
```yaml
parent:
  child: value
```

---

# 2. Kubernetes YAML Structure

Kubernetes uses YAML files to define **objects** such as Pods, Deployments, Services, etc.

Every Kubernetes YAML file typically has **four main fields**:

```
apiVersion
kind
metadata
spec
```

---

## 2.1 apiVersion

Defines **which version of Kubernetes API** you are using.

Examples:
- Pods → `v1`
- Deployments → `apps/v1`
- Services → `v1`

Example:
```yaml
apiVersion: apps/v1
```

---

## 2.2 kind

Defines **type of Kubernetes object**.

Examples:
- Pod
- Deployment
- Service
- ConfigMap
- Secret

Example:
```yaml
kind: Deployment
```

---

## 2.3 metadata

Contains identifying information such as:
- name
- namespace
- labels
- annotations

Example:
```yaml
metadata:
  name: my-app
  labels:
    app: demo
```

---

## 2.4 spec

Describes the **desired state** of the object.

Examples:
- For Pods → container details
- For Deployments → replicas, Pod template
- For Services → ports, selectors

Example:
```yaml
spec:
  replicas: 3
  template:
    ...
```

---

## 2.5 status (System Generated)

- Not written by users
- Auto-filled by Kubernetes
- Shows **actual state**

Example (auto-generated):
```yaml
status:
  availableReplicas: 3
  conditions:
    - type: Ready
```

---

# 3. Hands-on Exercises (Beginner Level)

## 3.1 Deploy NGINX Using Deployment

Create a file: `nginx-deployment.yaml`

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  replicas: 2
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
        - name: nginx
          image: nginx:1.25
          ports:
            - containerPort: 80
```

### Apply Deployment
```bash
kubectl apply -f nginx-deployment.yaml
kubectl get deployments
kubectl get pods -l app=nginx
```

---

## 3.2 Expose NGINX Deployment Using Service

Create a file: `nginx-service.yaml`

```yaml
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  type: ClusterIP
  selector:
    app: nginx
  ports:
    - port: 80
      targetPort: 80
```

### Apply Service
```bash
kubectl apply -f nginx-service.yaml
kubectl get svc
```

---

## 3.3 Scale Replicas

To scale Deployment:
```bash
kubectl scale deployment nginx-deployment --replicas=5
kubectl get deployments
```

To edit YAML and apply:
```bash
# update replicas: 5
kubectl apply -f nginx-deployment.yaml
```

---

