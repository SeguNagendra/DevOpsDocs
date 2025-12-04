---
sidebar_position: 9
---

# Kubernetes Services

This document provides a **detailed, production-level explanation of Kubernetes Services**
including **how they work internally, service types, YAML examples, troubleshooting,
and best practices**.

---

## 1. What is a Kubernetes Service?

A **Kubernetes Service** is an abstraction that provides:
- A **stable IP address**
- A **DNS name**
- **Load balancing** across Pods

Even though Pods are ephemeral (can be recreated with new IPs),  
a Service ensures **reliable communication**.

> Service = Stable network endpoint for a group of Pods

---

## 2. Why Do We Need Services?

### Problems Without Services
- Pod IPs change on restart
- No inbuilt load balancing
- Hardcoded IPs break applications

### With Services
✅ Stable endpoint  
✅ Service discovery via DNS  
✅ Built-in load balancing  

---

## 3. How Kubernetes Service Works (Internal Flow)

1. Pods are created with labels
2. Service selects Pods using label selectors
3. Endpoints / EndpointSlices are created
4. kube-proxy programs networking rules (iptables/IPVS)
5. Traffic is load-balanced to backend Pods

```
Client → Service IP → kube-proxy → Pod IPs
```

---

## 4. Core Service Components

### Labels & Selectors
Services **match Pods by labels**.

```yaml
selector:
  app: nginx
```

Only Pods with this label receive traffic.

---

### Endpoints / EndpointSlices
- Track Pod IPs behind a Service
- Updated dynamically when Pods scale or restart

```bash
kubectl get endpoints my-service
```

---

## 5. Service Types Overview

Kubernetes supports several Service types:

| Type | Scope | Use Case |
|----|------|---------|
| ClusterIP | Internal | Backend services |
| NodePort | External via Node | Labs / testing |
| LoadBalancer | External via cloud LB | Production |
| Headless | No LB | Stateful apps |
| ExternalName | External DNS | SaaS integration |

---

## 6. ClusterIP Service (Default)

### When to Use
- Internal communication only
- Microservice backend APIs
- Databases accessed internally

### Example YAML
```yaml
apiVersion: v1
kind: Service
metadata:
  name: nginx-clusterip
spec:
  type: ClusterIP
  selector:
    app: nginx
  ports:
    - port: 80
      targetPort: 80
```

### Access
```text
http://nginx-clusterip
```

---

## 7. NodePort Service

### When to Use
- Non-cloud clusters
- Development and testing
- Quick external exposure

### NodePort Range
```
30000 – 32767
```

### Example YAML
```yaml
apiVersion: v1
kind: Service
metadata:
  name: nginx-nodeport
spec:
  type: NodePort
  selector:
    app: nginx
  ports:
    - port: 80
      targetPort: 80
      nodePort: 30007
```

### Access
```text
http://<NodeIP>:30007
```

---

## 8. LoadBalancer Service

### When to Use
- Cloud environments (AWS, Azure, GCP)
- Production workloads

### Example YAML
```yaml
apiVersion: v1
kind: Service
metadata:
  name: nginx-lb
spec:
  type: LoadBalancer
  selector:
    app: nginx
  ports:
    - port: 80
      targetPort: 80
```

### Access
```text
http://<External-IP>
```

---

## 9. Headless Service

### What is Headless Service?
- No ClusterIP (`clusterIP: None`)
- Returns Pod IPs directly via DNS
- No load balancing by Service

### When to Use
- StatefulSets
- Databases
- Direct Pod-to-Pod communication

### Example YAML
```yaml
apiVersion: v1
kind: Service
metadata:
  name: mysql
spec:
  clusterIP: None
  selector:
    app: mysql
  ports:
    - port: 3306
```

### DNS Resolution
```text
mysql-0.mysql
mysql-1.mysql
```

---

## 10. ExternalName Service

### Purpose
Maps a Service to an **external DNS name**.

### Example YAML
```yaml
apiVersion: v1
kind: Service
metadata:
  name: external-api
spec:
  type: ExternalName
  externalName: api.example.com
```

---

## 11. Service vs Ingress

| Feature | Service | Ingress |
|------|--------|--------|
| OSI Layer | L4 (TCP/UDP) | L7 (HTTP/HTTPS) |
| Routing | Basic | Path/host-based |
| TLS | Limited | Native TLS |
| Use Case | Pod exposure | HTTP routing |

✅ In production: **Service + Ingress**

---

## 12. Full Example: Deployment + Service

### Deployment
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deploy
spec:
  replicas: 3
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
          image: nginx
          ports:
            - containerPort: 80
```

### Service
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

---

## 13. Troubleshooting Services

### Check Service
```bash
kubectl get svc
kubectl describe svc nginx-service
```

### Check Endpoints
```bash
kubectl get endpoints nginx-service
```

### Check Labels
```bash
kubectl get pods --show-labels
```

### Common Issues
- Selector does not match Pod labels
- Pods not in Ready state
- Wrong port or targetPort

---

## 14. Best Practices

✅ Use ClusterIP for internal services  
✅ Use Ingress for HTTP exposure  
✅ Avoid NodePort in production  
✅ Use Headless Services for StatefulSets  
✅ Always verify endpoints  

---

## 15. Interview One-Liners

- Services provide stable networking
- ClusterIP is default
- NodePort exposes via node IP
- LoadBalancer uses cloud LB
- Headless gives direct Pod IPs

---

## 16. Summary

- Services abstract Pod networking
- Enable discovery and load balancing
- Multiple Service types for different needs
- Essential for microservices

**Without Services, Kubernetes applications cannot communicate reliably.**

