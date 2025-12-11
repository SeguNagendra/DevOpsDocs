---
sidebar_position: 11
---


# K8s Ingress & Ingress Controller

This document provides an in-depth explanation of Kubernetes Ingress, Ingress Controllers, routing methods, and TLS with full YAML examples.

---

## 1. What is Ingress?

Ingress is a Kubernetes object that manages **external HTTP/HTTPS access** to internal cluster Services.  
It acts as a **Layer 7 router** and provides:
- URL path-based routing  
- Host-based routing  
- TLS/HTTPS termination  
- Central gateway for multiple services  

Pods and Services may change IPs, but Ingress gives a **stable entry point**.

---

## 2. Ingress vs Service

| Feature | Service (ClusterIP/NodePort/LB) | Ingress |
|--------|----------------------------------|---------|
| OSI Layer | L4 (TCP/UDP) | L7 (HTTP/HTTPS) |
| Routing | No URL routing | Path & host routing |
| TLS | Only with LoadBalancer | Full TLS support |
| External access | NodePort or LoadBalancer | Single LoadBalancer for many services |
| Best for | Basic access | Web routing |

---

## 3. What is an Ingress Controller?

Ingress **does nothing by itself**.  
You MUST install an **Ingress Controller**, such as:

### Popular Ingress Controllers
- **NGINX Ingress Controller** (most widely used)
- **Traefik**
- HAProxy
- Istio Gateway (via service mesh)

Example (Minikube install):
```bash
minikube addons enable ingress
```

---

## 4. Path-Based Routing

Route URLs to different services based on path.

### Example Routing
```
/app1 → app1-service
/app2 → app2-service
```

### YAML: Path-Based Ingress
```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: path-routing
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /
spec:
  rules:
    - http:
        paths:
          - path: /app1
            pathType: Prefix
            backend:
              service:
                name: app1-service
                port:
                  number: 80
          - path: /app2
            pathType: Prefix
            backend:
              service:
                name: app2-service
                port:
                  number: 80
```

---

## 5. Host-Based Routing

Used when different domain names map to different services.

### Example Routing
```
api.example.com → api-service  
ui.example.com → ui-service
```

### YAML: Host-Based Ingress
```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: host-routing
spec:
  rules:
    - host: api.example.com
      http:
        paths:
          - path: /
            pathType: Prefix
            backend:
              service:
                name: api-service
                port:
                  number: 80
    - host: ui.example.com
      http:
        paths:
          - path: /
            pathType: Prefix
            backend:
              service:
                name: ui-service
                port:
                  number: 80
```

---

## 6. TLS with Ingress (HTTPS)

Ingress can terminate TLS using certificates stored in secrets.

### Step 1: Create TLS Secret
```bash
kubectl create secret tls tls-secret   --cert=cert.crt   --key=cert.key
```

### Step 2: TLS Ingress YAML
```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: tls-ingress
spec:
  tls:
    - hosts:
        - secure.example.com
      secretName: tls-secret
  rules:
    - host: secure.example.com
      http:
        paths:
          - path: /
            pathType: Prefix
            backend:
              service:
                name: secure-service
                port:
                  number: 80
```

---

## 7. Full Example: Deployment + Service + Ingress

### Deployment
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: app1
spec:
  replicas: 2
  selector:
    matchLabels:
      app: app1
  template:
    metadata:
      labels:
        app: app1
    spec:
      containers:
        - name: app1
          image: nginx
          ports:
            - containerPort: 80
```

### Service
```yaml
apiVersion: v1
kind: Service
metadata:
  name: app1-service
spec:
  selector:
    app: app1
  ports:
    - port: 80
      targetPort: 80
```

### Ingress
```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: app1-ingress
spec:
  rules:
    - host: app1.example.com
      http:
        paths:
          - path: /
            pathType: Prefix
            backend:
              service:
                name: app1-service
                port:
                  number: 80
```

---

## 8. Troubleshooting Ingress

### Check Ingress
```bash
kubectl get ingress
```

### Describe Ingress
```bash
kubectl describe ingress <name>
```

### Check Ingress Controller pods
```bash
kubectl get pods -n ingress-nginx
```

### If EXTERNAL-IP is pending:
For Minikube:
```bash
minikube tunnel
```

### Check service endpoints
```bash
kubectl get endpoints
```

---

## 9. Best Practices

- Use **Ingress + ClusterIP services** for production apps  
- Do not expose workloads using NodePort in production  
- Use TLS for all public routes  
- Use host-based routing for microservices  
- Prefer NGINX or Traefik controllers  

---

# Summary

Ingress provides:
- Clean HTTP routing
- TLS termination
- Single entry point
- Cost-efficient routing for many services

Ingress Controller executes the routing rules.  
Together, they form the foundation of modern Kubernetes web application delivery.

