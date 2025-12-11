---
sidebar_position: 15
---


# Kubernetes Health Checks

This document explains **Liveness**, **Readiness**, and **Startup** probes in Kubernetes with detailed explanations, diagrams, and real-world YAML examples.

---

# 1. Why Health Checks Are Needed in Kubernetes

Containers may:
- Start slowly  
- Become unresponsive  
- Crash internally but not exit  
- Be able to start serving traffic only after initialization  

Kubernetes uses **probes** to determine:
- When a container is ready  
- When it must be restarted  
- When it should start receiving traffic  

Probes keep applications **self-healing**, **reliable**, and **highly available**.

---

# 2. Types of Probes

| Probe Type | Purpose | Action Taken |
|------------|---------|--------------|
| **Liveness Probe** | Is the application alive? | Restart container if probe fails |
| **Readiness Probe** | Is the app ready to accept traffic? | Remove Pod from Service endpoints |
| **Startup Probe** | Did the app finish startup? | Protect slow apps from early liveness failures |

---

# 3. Liveness Probe (Detect & Restart Dead Containers)

A **liveness probe** checks if the application is healthy *during runtime*.  
If it fails → Kubernetes **restarts** the container.

### When to use?
- App becomes stuck or hangs  
- Deadlocks  
- Long-running connections that freeze  

---

## 3.1 Liveness Probe Example — HTTP Check

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: liveness-demo
spec:
  containers:
    - name: app
      image: nginx
      livenessProbe:
        httpGet:
          path: /
          port: 80
        initialDelaySeconds: 5
        periodSeconds: 10
```

Meaning:
- Starts checking after **5 seconds**
- Probes endpoint **every 10 seconds**
- If 3 consecutive failures → Pod auto-restarts

---

## 3.2 Liveness Probe Example — Exec Command

```yaml
livenessProbe:
  exec:
    command: ["sh", "-c", "pidof nginx"]
  initialDelaySeconds: 5
```

If command returns non‑zero status → Kubernetes restarts container.

---

## 3.3 Liveness Probe Example — TCP Check

```yaml
livenessProbe:
  tcpSocket:
    port: 3306
```

Useful for databases.

---

# 4. Readiness Probe (Controls Traffic Flow)

A **readiness probe** checks if a Pod is **ready to accept traffic**.  
If it fails → Pod is *removed* from Service endpoints.

### Pod is NOT restarted, only traffic is stopped.

---

## When to use Readiness Probes?
- App needs warm-up time  
- Waiting for DB connection  
- Loading large internal caches  
- Partial outages (app running but not fully ready)

---

## 4.1 Readiness Probe Example

```yaml
readinessProbe:
  httpGet:
    path: /ready
    port: 8080
  initialDelaySeconds: 3
  periodSeconds: 5
```

If readiness probe fails:
- Pod stays **Running**
- BUT Service stops sending traffic to it

This prevents:
- Bad user requests
- Failed responses
- Rolling updates from taking down all Pods at once

---

# 5. Startup Probe (For Slow-Starting Applications)

Some applications take a long time to boot:
- Java Spring Boot apps  
- Large microservices  
- Machine learning services  

If LivenessProbe runs too early → Kubernetes restarts app unnecessarily.

### Startup probe prevents this.

---

## 5.1 Startup Probe Example

```yaml
startupProbe:
  httpGet:
    path: /health
    port: 8080
  failureThreshold: 30
  periodSeconds: 10
```

Meaning:
- Kubernetes gives app **30 × 10 = 300 seconds** to start
- Liveness probe begins ONLY after startup probe succeeds

---

# 6. How Probes Work Together

### Correct sequence:
```
Startup → Liveness → Readiness
```

- **Startup probe**: Ensures the app boots before other probes run  
- **Liveness probe**: Ensures the app stays healthy  
- **Readiness probe**: Ensures app receives traffic only when ready  

---

# 7. Full Example: All Probes Together

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: full-probe-demo
spec:
  containers:
    - name: app
      image: myapp:latest

      startupProbe:
        httpGet:
          path: /startup
          port: 8080
        failureThreshold: 30
        periodSeconds: 5

      livenessProbe:
        httpGet:
          path: /health
          port: 8080
        initialDelaySeconds: 5
        periodSeconds: 10

      readinessProbe:
        httpGet:
          path: /ready
          port: 8080
        initialDelaySeconds: 3
        periodSeconds: 5
```

Behavior:
- Pod gets **up to 150 seconds** to start  
- After startup is successful → Liveness begins monitoring  
- When ready → Service starts sending traffic  

---

# 8. Common Failure Scenarios & Fixes

### ❌ Issue 1: Liveness probe restarts app repeatedly  
**Cause:** App takes long to start  
**Fix:** Add **startupProbe**

---

### ❌ Issue 2: Pod stays running but receives no traffic  
**Cause:** Readiness probe failing  
**Fix:** Check logs, verify `/ready` endpoint

---

### ❌ Issue 3: Probes hitting wrong port  
Check with:
```bash
kubectl describe pod <name>
```

---

### ❌ Issue 4: App slow under high load  
Readiness probes may fail → Pod temporarily removed from load balancer  
This is good for reliability.

---

# 9. Best Practices

- Always define readinessProbe for production apps  
- Use startupProbe for Java/.NET/slow workloads  
- Do not make probes too aggressive  
- Never use same endpoint for liveness & readiness  
- Liveness should check something lightweight  
- Readiness should check full dependencies (DB, cache, etc.)

---

# 10. Summary

| Probe Type | Purpose | Action |
|------------|----------|--------|
| **Startup Probe** | Ensure app boot completes | Blocks liveness until ready |
| **Liveness Probe** | Detect dead/hung app | Restarts Pod |
| **Readiness Probe** | Accepting traffic or not? | Adds/removes Pod from LB |

Probes make Kubernetes:
- Reliable  
- Highly available  
- Auto-healing  
- Safe during deployments  

---


# Kubernetes Health Checks – Hands‑On Labs (With Expected Output)

This document provides **practical labs** for:
- Liveness Probe  
- Readiness Probe  
- Startup Probe  

Each lab includes:

✔ YAML manifest  
✔ Step-by-step commands  
✔ Expected output  
✔ Troubleshooting tips  

---

# LAB 1 — Liveness Probe (Detect & Restart Crashed Containers)

## Objective
Demonstrate how a liveness probe restarts a container when an internal process fails.

---

## Step 1 — Pod With Liveness Probe
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: liveness-lab
spec:
  containers:
    - name: app
      image: busybox
      command:
        - sh
        - -c
        - >
          touch /tmp/healthy;
          while true; do
            if [ -f /tmp/healthy ]; then
              echo "I am healthy";
            else
              echo "I am NOT healthy";
            fi;
            sleep 5;
          done
      livenessProbe:
        exec:
          command: ["test", "-f", "/tmp/healthy"]
        initialDelaySeconds: 5
        periodSeconds: 5
```

---

## Step 2 — Deploy the Pod
```bash
kubectl apply -f liveness-lab.yaml
kubectl get pods
```

---

## Step 3 — Break Liveness Condition
```bash
kubectl exec liveness-lab -- rm /tmp/healthy
```

---

## Expected Output
```bash
kubectl describe pod liveness-lab
```

You’ll see:
```
Liveness probe failed
Killing container
Container restarted
```

Pod `RESTARTS` — confirming liveness works.

---

# LAB 2 — Readiness Probe (Control Traffic Routing)

## Objective
Show how a readiness probe stops sending traffic to a Pod when it is not ready.

---

## Step 1 — Pod with Readiness Probe
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: readiness-lab
  labels:
    app: web
spec:
  containers:
    - name: app
      image: busybox
      command:
        - sh
        - -c
        - >
          echo "Starting app...";
          sleep 30;
          touch /tmp/ready;
          sleep 300;
      readinessProbe:
        exec:
          command: ["test", "-f", "/tmp/ready"]
        initialDelaySeconds: 2
        periodSeconds: 3
```

---

## Step 2 — Deploy the Pod
```bash
kubectl apply -f readiness-lab.yaml
```

---

## Step 3 — Watch Probe Status
```bash
kubectl get pod readiness-lab -w
```

---

## Expected Behavior
For first 30 seconds:
```
READY 0/1
```

After probe succeeds:
```
READY 1/1
```

Pod will begin receiving traffic **only when ready**.

---

# LAB 3 — Startup Probe (Protect Slow Boot Apps)

## Objective
Demonstrate how startup probes prevent premature liveness failures.

---

## Step 1 — Pod With Startup + Liveness Probe
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: startup-lab
spec:
  containers:
    - name: app
      image: busybox
      command:
        - sh
        - -c
        - >
          echo "Booting...";
          sleep 40;
          touch /tmp/started;
          sleep 300;
      startupProbe:
        exec:
          command: ["test", "-f", "/tmp/started"]
        failureThreshold: 10
        periodSeconds: 5
      livenessProbe:
        exec:
          command: ["test", "-f", "/tmp/started"]
        initialDelaySeconds: 1
        periodSeconds: 5
```

---

## Explanation
- App takes **40 seconds** to start  
- StartupProbe allows **50 seconds** (10×5s)  
- Liveness probe begins ONLY after startup succeeds  

---

## Step 2 — Deploy and Watch Logs
```bash
kubectl apply -f startup-lab.yaml
kubectl describe pod startup-lab
```

---

## Expected Output
During first 40 sec:
```
Startup probe still failing...
```

After the file appears:
```
Startup probe succeeded!!
Liveness probe starts
```

Pod does NOT restart — proving startup probe works.

---

# LAB 4 — All Probes + Service

## Objective
Understand interaction of probes with load balancing.

---

### YAML Example
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: probes-lab
  labels:
    app: demo
spec:
  containers:
    - name: app
      image: nginx

      startupProbe:
        httpGet:
          path: /
          port: 80
        failureThreshold: 30
        periodSeconds: 5

      livenessProbe:
        httpGet:
          path: /
          port: 80
        initialDelaySeconds: 5
        periodSeconds: 10

      readinessProbe:
        httpGet:
          path: /
          port: 80
        initialDelaySeconds: 2
        periodSeconds: 5
---
apiVersion: v1
kind: Service
metadata:
  name: demo-svc
spec:
  selector:
    app: demo
  ports:
    - port: 80
```

---

### Expected Behavior
- Pod joins service **only after readiness succeeds**  
- If liveness fails → Pod restarts  
- Startup probe protects slow starts  

---

# Troubleshooting Guide

### ❌ Pod restarting repeatedly  
Cause: liveness probe failing  
Fix: adjust `initialDelaySeconds`, or add a startup probe  

---

### ❌ Pod never becomes ready  
Cause:
- Wrong readiness endpoint  
- App not starting dependencies  

Check:
```bash
kubectl logs pod <name>
kubectl describe pod <name>
```

---

### ❌ Service not routing traffic to Pod  
Check readiness:
```bash
kubectl get endpoints demo-svc
```

---

# Summary

| Probe | Purpose | Failure Effect |
|-------|----------|----------------|
| **Startup** | Ensure slow apps boot fully | Delays other probes |
| **Liveness** | Detect dead app | Restarts Pod |
| **Readiness** | Allow traffic only when ready | Removes Pod from LB |

Probes make Kubernetes **self-healing**, **reliable**, and **safe for rolling updates**.




