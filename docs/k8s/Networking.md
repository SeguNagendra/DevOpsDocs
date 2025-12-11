---
sidebar_position: 17
---


# Kubernetes Networking 
## CNI, Pod Networking, Services & DNS

This document provides a **clean, structured, and detailed** explanation of Kubernetes networking, covering:

- CNI Plugins (Calico, Flannel, Cilium)
- Pod-to-Pod networking
- Service networking
- DNS in Kubernetes (CoreDNS)

---

# 1. Kubernetes Networking Deep Dive

Kubernetes networking is based on two core principles:

1. **Every Pod gets its own unique IP address.**  
2. **Pods must communicate with each other without NAT.**

This eliminates port conflicts seen in Docker and simplifies service discovery.

---

# 2. CNI Plugins in Kubernetes

Kubernetes does NOT implement networking itself.  
Instead, it relies on **CNI (Container Network Interface)** plugins to provide Pod networking.

CNI responsibilities:

- Assign Pod IP addresses
- Manage routing
- Connect Pods across nodes
- Enforce NetworkPolicies (if supported)

---

## 2.1 Flannel – Simple Overlay Network

**Flannel** is the simplest CNI focused on network connectivity.

### Key Features:
- Uses **VXLAN** or **host-gw** for overlay routing
- Easy to set up
- Suitable for small to medium clusters

### How it works:
- Each node gets a subnet, e.g., `10.244.1.0/24`
- Pods on that node receive IPs from the subnet
- VXLAN tunnels route traffic cross-node

Example IP allocation:
```
Node 1 → 10.244.1.0/24
Node 2 → 10.244.2.0/24
```

---

## 2.2 Calico – Enterprise-Grade Networking + Policies

**Calico** provides:

- Layer 3 pure routing (no overlays)
- Optional BGP support
- Advanced NetworkPolicy capabilities
- Best performance among CNIs

### When to use:
- Large clusters
- Need for strong network security
- Want to use NetworkPolicies extensively

---

## 2.3 Cilium – eBPF Powered High Performance CNI

**Cilium** uses eBPF instead of iptables for networking & security.

### Features:
- High performance dataplane
- Transparent encryption
- NetworkPolicy enforcement using eBPF
- Deep observability and metrics
- Service mesh mode without sidecars

### Ideal For:
- High-performance clusters
- Low-latency networking workloads
- Cloud native microservices

---

# 3. Pod-to-Pod Networking

Pods have:
- Unique IP addresses
- A **virtual ethernet interface (veth)**
- A shared network namespace within the Pod

---

## 3.1 Pod-to-Pod on the Same Node

```
Pod A → vethA → cni0 bridge → vethB → Pod B
```

Traffic stays entirely inside the node.

---

## 3.2 Pod-to-Pod Across Different Nodes

Example:
- Pod A (Node 1): `10.244.1.12`
- Pod B (Node 2): `10.244.2.22`

Traffic flow:
```
Pod A → Node 1 CNI → Overlay/BGP routing → Node 2 CNI → Pod B
```

Calico/Cilium may use routing instead of overlays, improving performance.

---

# 4. Service Networking

Pod IPs are **ephemeral**, so Kubernetes Services provide stable endpoints.

### Service Types:
| Type | Purpose |
|------|---------|
| **ClusterIP** | Internal service communication |
| **NodePort** | Expose service on each node |
| **LoadBalancer** | Cloud LB forwarding to nodes |
| **Headless Service** | Direct Pod IP discovery |

---

## 4.1 ClusterIP Service (Most Common)

```yaml
apiVersion: v1
kind: Service
metadata:
  name: backend
spec:
  selector:
    app: backend
  ports:
    - port: 80
      targetPort: 8080
```

Traffic flow:
```
Pod → ClusterIP → kube-proxy → Pod endpoints
```

---

## 4.2 NodePort Service

Exposes service on every node:

```
<NodeIP>:30080 → Service → Pods
```

Used mainly for:
- Local clusters
- Bare-metal without LB

---

## 4.3 LoadBalancer Service

Used in cloud environments:

```
Internet → Cloud LB → NodePort → kube-proxy → Pods
```

---

## 4.4 Headless Service (clusterIP: None)

Allows direct access to Pod IPs.

Used for:
- StatefulSets
- Databases (MySQL, Cassandra, Redis)

Example:
```yaml
clusterIP: None
```

DNS resolves to Pod IPs instead of a virtual ClusterIP.

---

# 5. DNS in Kubernetes (CoreDNS)

CoreDNS handles internal DNS resolution.

### Responsibilities:
- Service discovery
- Pod DNS records
- Custom DNS plugins
- Internal cluster domain management

Default DNS name format:
```
<service>.<namespace>.svc.cluster.local
```

Example:
```
backend.default.svc.cluster.local
```

---

## 5.1 DNS Example: Resolve Service Name

Inside a Pod:
```bash
nslookup backend
```

Output:
```
Name: backend.default.svc.cluster.local
Address: 10.96.0.12
```

---

## 5.2 DNS for Headless Services

```bash
nslookup db.default.svc.cluster.local
```

Returns:
```
10.244.1.10
10.244.2.12
```

Each Pod has its own record.

---

# 6. End-to-End Networking Flow Diagram

### Pod → Pod
```
Pod → veth → CNI Bridge → Node routing → CNI Overlay/BGP → Pod
```

### Pod → Service
```
Pod → Service IP → kube-proxy (iptables/IPVS) → Pod endpoints
```

### Pod → External
```
Pod → Node NAT (MASQUERADE) → Internet
```

---

# 7. Troubleshooting Networking

### Check Pod IPs
```bash
kubectl get pods -o wide
```

### Test DNS
```bash
kubectl exec -it pod -- nslookup backend
```

### Check Service Endpoints
```bash
kubectl get endpoints backend
```

### Inspect CNI plugin
```bash
kubectl get pods -n kube-system
```

---

# 8. Summary

| Component | Purpose |
|-----------|---------|
| **CNI Plugin** | Provides Pod networking |
| **Pod-to-Pod Networking** | Direct communication using Pod IPs |
| **Service Networking** | Stable access via Service IP |
| **DNS (CoreDNS)** | Internal service discovery |

Kubernetes networking is powerful because it provides **consistent, NAT-less Pod connectivity**, with scalable service discovery and strong policy enforcement.

---


# Kubernetes Networking – Hands-On Labs + Service Mesh (Istio & Linkerd) Deep Dive  
This document provides practical, step-by-step labs with expected outputs for Kubernetes networking, PLUS detailed explanations of **Service Mesh networking (Istio & Linkerd)**.

---

# 🔥 SECTION 1 — Kubernetes Networking Hands‑On Labs (With Expected Outputs)

These labs teach real‑world Kubernetes networking behaviour.

---

# LAB 1 — Pod‑to‑Pod Connectivity

## Objective
Verify Pod communication using Pod IPs.

---

## Step 1: Deploy Two Pods

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: pod-a
  labels:
    app: a
spec:
  containers:
    - name: app
      image: busybox
      command: ["sh", "-c", "sleep 3600"]

---
apiVersion: v1
kind: Pod
metadata:
  name: pod-b
  labels:
    app: b
spec:
  containers:
    - name: app
      image: busybox
      command: ["sh", "-c", "sleep 3600"]
```

Apply:
```bash
kubectl apply -f pods.yaml
```

---

## Step 2: Get Pod IPs
```bash
kubectl get pods -o wide
```

Expected output (example):
```
pod-a   10.244.1.10
pod-b   10.244.2.15
```

---

## Step 3: Connect from Pod A → Pod B

```bash
kubectl exec -it pod-a -- ping -c 3 10.244.2.15
```

Expected output:
```
3 packets transmitted, 3 received, 0% packet loss
```

🎉 **Conclusion:** Pod‑to‑Pod communication works across nodes.

---

# LAB 2 — ClusterIP Service Networking

## Objective
Test Service → Pod routing using kube‑proxy.

---

## Step 1: Deploy a Simple App

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: web
  labels:
    app: web
spec:
  containers:
    - name: web
      image: nginx
```

---

## Step 2: Create ClusterIP Service

```yaml
apiVersion: v1
kind: Service
metadata:
  name: web-svc
spec:
  selector:
    app: web
  ports:
    - port: 80
      targetPort: 80
```

---

## Step 3: Test Service Connectivity

```bash
kubectl run test --rm -it --image=busybox -- sh
wget -qO- http://web-svc
```

Expected output:
```
<!DOCTYPE html>
<html>
<head><title>Welcome to nginx!</title></head>
```

🎉 **Conclusion:** ClusterIP load‑balancing works.

---

# LAB 3 — NodePort Service Networking

## Step 1: Expose Service as NodePort

```yaml
apiVersion: v1
kind: Service
metadata:
  name: web-nodeport
spec:
  type: NodePort
  selector:
    app: web
  ports:
    - port: 80
      nodePort: 30080
```

---

## Step 2: Get Node IP

```bash
kubectl get nodes -o wide
```

---

## Step 3: Curl NodePort

```
curl http://<NodeIP>:30080
```

Expected: Nginx homepage.

🎉 **Conclusion:** NodePort exposes service externally.

---

# LAB 4 — DNS + CoreDNS Testing

## Step 1: Create a Service

Service name: **backend**

```bash
nslookup backend
```

Expected:
```
Name: backend.default.svc.cluster.local
Address: 10.96.0.15
```

---

## Step 2: Test Pod‑Level DNS Resolution

Inside any Pod:
```bash
wget -qO- http://backend
```

Expected: App response.

🎉 **Conclusion:** CoreDNS correctly resolves Services.

---

# LAB 5 — NetworkPolicy Enforcement

## Step 1: Default Deny Policy

```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: deny-all
spec:
  podSelector: {}
  policyTypes:
    - Ingress
```

Effect:
- All incoming traffic is blocked.

---

## Step 2: Allow Only Pod A → Pod B

```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: allow-a-to-b
spec:
  podSelector:
    matchLabels:
      app: b
  ingress:
    - from:
        - podSelector:
            matchLabels:
              app: a
```

Test:
```
kubectl exec pod-a -- wget -qO- http://pod-b
kubectl exec pod-c -- wget -qO- http://pod-b
```

Expected:
```
pod-a → pod-b = SUCCESS
pod-c → pod-b = BLOCKED
```

🎉 **Conclusion:** NetworkPolicy isolates traffic.

---

# 🔥 SECTION 2 — Service Mesh Networking (Istio & Linkerd)

Service Mesh provides:
- mTLS encryption
- Traffic shifting
- Observability (metrics, tracing)
- Retries, circuit breaking
- Service-to-service authorization

---

# 1. Istio – Deep Explanation

Istio uses **sidecar proxy (Envoy)** injected into every Pod.

---

## 1.1 Istio Architecture

```
App Pod — Envoy Sidecar → Mesh Network → Envoy → App Pod
```

Control plane:
- istiod: config, certificates, routing rules

Data plane:
- Envoy sidecar proxies

---

## 1.2 Install Istio (profile=demo)

```bash
istioctl install --set profile=demo -y
```

Enable automatic sidecar injection:

```bash
kubectl label namespace default istio-injection=enabled
```

---

## 1.3 Example Application With Istio

### Deploy App

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: istio-app
spec:
  replicas: 2
  selector:
    matchLabels:
      app: istio-app
  template:
    metadata:
      labels:
        app: istio-app
    spec:
      containers:
        - name: app
          image: nginx
```

Pods now contain **Envoy sidecars**.

Check:
```bash
kubectl get pods
```

You will see:
```
istio-app-xxx   2/2   Running
```

---

## 1.4 Istio VirtualService Example (Traffic Routing)

```yaml
apiVersion: networking.istio.io/v1alpha3
kind: VirtualService
metadata:
  name: app-route
spec:
  hosts:
    - istio-app
  http:
    - route:
        - destination:
            host: istio-app
            subset: v1
```

---

## 1.5 Istio mTLS Example

```yaml
apiVersion: security.istio.io/v1beta1
kind: PeerAuthentication
metadata:
  name: default
spec:
  mtls:
    mode: STRICT
```

All Pod-to-Pod traffic is now encrypted.

---

# 2. Linkerd – Deep Explanation

Linkerd focuses on:
- Lightweight sidecar proxy (rust-based)
- Auto mTLS for all connections
- Extremely low latency overhead

---

## 2.1 Install Linkerd

```bash
linkerd install | kubectl apply -f -
linkerd viz install | kubectl apply -f -
```

Check:
```bash
linkerd check
```

---

## 2.2 Inject Sidecars Into Pods

```bash
kubectl get deploy web -o yaml | linkerd inject - | kubectl apply -f -
```

---

## 2.3 Linkerd Traffic Metrics Example

```
linkerd viz stat deploy
```

Example output:
```
NAME      SUCCESS   RPS   LATENCY
web       99.9%     10    5ms
```

---

## 2.4 Linkerd mTLS

Check status:
```
linkerd viz edges deploy
```

Expected:
```
TLS = True
```

---

# 3. Istio vs Linkerd – Comparison

| Feature | Istio | Linkerd |
|---------|--------|----------|
| Architecture | Complex | Simple |
| Proxy | Envoy | Rust micro-proxy |
| mTLS | Manual config | Automatic |
| Performance | Medium | Very high |
| Ideal for | Large enterprises | Simple secure meshes |

---

# Summary

You learned:

✔ Pod-to-Pod connectivity  
✔ Service networking  
✔ DNS resolution  
✔ NetworkPolicies  
✔ Istio routing, mTLS, VirtualService  
✔ Linkerd auto‑mTLS & metrics  

---

