---
sidebar_position: 10
---

## 1. What is Configuration Management in Kubernetes?

**Configuration Management** in Kubernetes is the practice of **separating application configuration from application code** so that the same container image can be used across multiple environments such as **Dev, QA, UAT, and Production**.

In Kubernetes, configuration management allows you to:
- Change behavior of applications **without rebuilding images**
- Store environment-specific values outside the container
- Manage sensitive and non-sensitive settings securely
- Update configurations independently of application code

---

## 2. Why Configuration Management is Needed

Without configuration management:
- Configuration values are hardcoded in application code
- Different Docker images are required for each environment
- Secrets (passwords, tokens) may get exposed
- Application becomes difficult to manage and scale

With Kubernetes configuration management:
- ✅ One container image for all environments
- ✅ Secure handling of sensitive data
- ✅ Easier updates and rollbacks
- ✅ Better DevOps and GitOps workflows

---

## 3. Kubernetes Configuration Management Building Blocks

Kubernetes provides the following primitives:
- **ConfigMaps** → Non-sensitive configuration
- **Secrets** → Sensitive configuration
- **Environment Variables**
- **Mounted Configuration Files**

---

## 4. Environment Variables in Kubernetes

### 4.1 What Are Environment Variables?

Environment variables are **key–value pairs** injected into containers at runtime. Applications read these variables to determine how they should behave.

Examples:
- Application environment (dev / prod)
- Log levels
- Service URLs
- Feature flags

---

### 4.2 Setting Environment Variables Directly

```yaml
env:
  - name: APP_ENV
    value: production
  - name: LOG_LEVEL
    value: info
```

✅ Simple but not reusable  
❌ Not recommended for large deployments  

---

### 4.3 Environment Variables Using ConfigMap

**ConfigMap**
```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: app-config
data:
  APP_ENV: production
  LOG_LEVEL: info
```

**Deployment**
```yaml
envFrom:
  - configMapRef:
      name: app-config
```

✅ Most common approach  
✅ Clean and reusable  

---

### 4.4 Environment Variables Using Secret

**Secret**
```yaml
apiVersion: v1
kind: Secret
metadata:
  name: db-secret
type: Opaque
data:
  DB_USER: YWRtaW4=
  DB_PASSWORD: cGFzcw==
```

**Deployment**
```yaml
envFrom:
  - secretRef:
      name: db-secret
```

✅ Secure for sensitive data  
❌ Requires Pod restart when values change  

---

### 4.5 Key Characteristics of Environment Variables

| Feature | Behavior |
|------|--------|
| Update after change | ❌ Pod restart required |
| Visibility | Visible via `kubectl describe pod` |
| Best for | Small configuration values |

---

## 5. Mounted Configurations in Kubernetes

### 5.1 What Are Mounted Configs?

Mounted configurations expose **ConfigMaps or Secrets as files inside containers** using volumes.

Each key becomes a file:
- Filename = key name
- File content = value

---

### 5.2 Mounting ConfigMap as Files

**ConfigMap**
```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: file-config
data:
  app.properties: |
    app.name=demo
    app.env=prod
```

**Deployment**
```yaml
volumes:
  - name: config-volume
    configMap:
      name: file-config

volumeMounts:
  - name: config-volume
    mountPath: /etc/config
```

**Inside container**
```text
/etc/config/app.properties
```

✅ Best for file-based configs  
✅ Changes reflect automatically  

---

### 5.3 Mounting Secrets as Files

**Secret**
```yaml
apiVersion: v1
kind: Secret
metadata:
  name: tls-secret
type: Opaque
data:
  password: c2VjcmV0
```

**Deployment**
```yaml
volumes:
  - name: secret-volume
    secret:
      secretName: tls-secret

volumeMounts:
  - name: secret-volume
    mountPath: /etc/secret
    readOnly: true
```

✅ More secure than env vars  
✅ Common for certificates and keys  

---

### 5.4 Key Characteristics of Mounted Configs

| Feature | Behavior |
|------|--------|
| Update after change | ✅ Auto-updated |
| Visibility | Filesystem only |
| Best for | Large configs, certs |

---

## 6. Complete Example: Config Management Using Env Vars + Mounted Configs

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: demo-config
data:
  APP_ENV: production
  LOG_LEVEL: info
---
apiVersion: v1
kind: Secret
metadata:
  name: demo-secret
type: Opaque
data:
  DB_PASSWORD: cGFzc3dvcmQ=
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: demo-app
spec:
  replicas: 2
  selector:
    matchLabels:
      app: demo
  template:
    metadata:
      labels:
        app: demo
    spec:
      containers:
        - name: app
          image: nginx
          envFrom:
            - configMapRef:
                name: demo-config
            - secretRef:
                name: demo-secret
          volumeMounts:
            - name: config-vol
              mountPath: /etc/app-config
            - name: secret-vol
              mountPath: /etc/app-secret
              readOnly: true
      volumes:
        - name: config-vol
          configMap:
            name: demo-config
        - name: secret-vol
          secret:
            secretName: demo-secret
```

---

## 7. Best Practices for Kubernetes Configuration Management

- ✅ Never hardcode configuration
- ✅ Use ConfigMaps for non-sensitive data
- ✅ Use Secrets for sensitive data
- ✅ Use environment variables for small configs
- ✅ Use mounted files for large or dynamic configs
- ✅ Separate configurations by namespaces
- ✅ Enable encryption at rest for Secrets
- ✅ Use GitOps tools (Argo CD, Flux)

---

## 8. Summary

Kubernetes configuration management:
- Separates code from configuration
- Enables environment-based deployments
- Improves security and flexibility
- Is essential for production-grade Kubernetes systems


# Kubernetes ConfigMap & Secret 

This document explains **ConfigMaps** and **Secrets** in detail and shows a **complete Deployment example** that uses both.

---

## 1. ConfigMap – Detailed View

A **ConfigMap** is used to store **non-sensitive** configuration data as key–value pairs.

Typical use cases:
- App configuration (environment, log level)
- Feature flags
- Hostnames, URLs, ports
- File-based configuration (e.g., `app.properties`, `nginx.conf`)

### 1.1 ConfigMap Structure

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: app-config
data:
  APP_NAME: "demo-app"
  APP_ENV: "production"
  LOG_LEVEL: "info"
  WELCOME_MESSAGE: "Welcome to the demo application!"
```

Key points:
- `data` holds string key–value pairs
- Keys must be valid DNS subdomain names or simple strings without spaces
- Values are strings (can hold JSON, YAML, etc.)

### 1.2 Ways to Create a ConfigMap

**From literal values:**
```bash
kubectl create configmap app-config   --from-literal=APP_NAME=demo-app   --from-literal=LOG_LEVEL=info
```

**From a file:**
```bash
kubectl create configmap app-config --from-file=config.properties
```

**From YAML (recommended for GitOps):**
```bash
kubectl apply -f app-config.yaml
```

### 1.3 Using ConfigMaps in Pods

You can use ConfigMaps in **three main ways**:

#### A. As Environment Variables (common)

```yaml
envFrom:
  - configMapRef:
      name: app-config
```

#### B. As Specific Environment Variables (fine-grained)

```yaml
env:
  - name: APP_NAME
    valueFrom:
      configMapKeyRef:
        name: app-config
        key: APP_NAME
```

#### C. As Mounted Files

```yaml
volumes:
  - name: config-volume
    configMap:
      name: app-config

volumeMounts:
  - name: config-volume
    mountPath: /etc/app-config
```

> Each key in the ConfigMap becomes a file under `/etc/app-config`.

---

## 2. Secret – Detailed View

A **Secret** stores **sensitive** data such as:
- Passwords
- API tokens
- Certificates
- SSH keys

### 2.1 Secret Structure

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: db-credentials
type: Opaque
data:
  DB_USERNAME: YWRtaW4=       # "admin" (base64)
  DB_PASSWORD: cGFzc3dvcmQ=   # "password" (base64)
```

> Note: Values in `data` **must be base64 encoded**.

You can generate base64 strings like this:

```bash
echo -n "admin" | base64
echo -n "password" | base64
```

### 2.2 Ways to Create a Secret

**From literals:**
```bash
kubectl create secret generic db-credentials   --from-literal=DB_USERNAME=admin   --from-literal=DB_PASSWORD=password
```

**From files:**
```bash
kubectl create secret generic tls-secret   --from-file=tls.crt=path/to/tls.crt   --from-file=tls.key=path/to/tls.key
```

**From YAML (recommended):**
```bash
kubectl apply -f db-credentials.yaml
```

### 2.3 Using Secrets in Pods

#### A. As Environment Variables

```yaml
envFrom:
  - secretRef:
      name: db-credentials
```

#### B. As Specific Environment Variables

```yaml
env:
  - name: DB_USER
    valueFrom:
      secretKeyRef:
        name: db-credentials
        key: DB_USERNAME
```

#### C. As Mounted Files (common for TLS)

```yaml
volumes:
  - name: db-secret-volume
    secret:
      secretName: db-credentials

volumeMounts:
  - name: db-secret-volume
    mountPath: /etc/db-secret
    readOnly: true
```

---

## 3. Full Example: Deployment Using ConfigMap & Secret

### Scenario

We have a demo web application that:

- Reads general app settings from a **ConfigMap**
- Reads database credentials from a **Secret**
- Exposes the application via a **Service**

We will create:

1. `ConfigMap` → App configuration  
2. `Secret` → Database username & password  
3. `Deployment` → Uses both ConfigMap & Secret  
4. `Service` → Exposes the app internally  

> All in a **single YAML file** using `---` separators.

---

### 3.1 Complete YAML Manifest

```yaml
# 1. ConfigMap: Non-sensitive configuration
apiVersion: v1
kind: ConfigMap
metadata:
  name: demo-app-config
data:
  APP_NAME: "k8s-config-demo"
  APP_ENV: "production"
  LOG_LEVEL: "info"
  WELCOME_MESSAGE: "Welcome to the Kubernetes Config Demo!"

---

# 2. Secret: Sensitive configuration (DB credentials)
apiVersion: v1
kind: Secret
metadata:
  name: demo-db-secret
type: Opaque
data:
  DB_USERNAME: YWRtaW4=       # "admin"
  DB_PASSWORD: cGFzc3dvcmQ=   # "password"

---

# 3. Deployment: Uses both ConfigMap & Secret
apiVersion: apps/v1
kind: Deployment
metadata:
  name: demo-app-deployment
spec:
  replicas: 2
  selector:
    matchLabels:
      app: demo-app
  template:
    metadata:
      labels:
        app: demo-app
    spec:
      containers:
        - name: demo-app-container
          image: nginx:1.25
          ports:
            - containerPort: 80

          # A. Load all keys from ConfigMap as environment variables
          envFrom:
            - configMapRef:
                name: demo-app-config

          # B. Load all keys from Secret as environment variables
            - secretRef:
                name: demo-db-secret

          # C. Load specific keys from ConfigMap and Secret explicitly
          env:
            - name: APP_NAME_EXPLICIT
              valueFrom:
                configMapKeyRef:
                  name: demo-app-config
                  key: APP_NAME

            - name: DB_USER_EXPLICIT
              valueFrom:
                secretKeyRef:
                  name: demo-db-secret
                  key: DB_USERNAME

          # D. Mount ConfigMap as files
          volumeMounts:
            - name: config-volume
              mountPath: /etc/demo-config

            - name: secret-volume
              mountPath: /etc/demo-secret
              readOnly: true

      volumes:
        # ConfigMap volume
        - name: config-volume
          configMap:
            name: demo-app-config

        # Secret volume
        - name: secret-volume
          secret:
            secretName: demo-db-secret

---

# 4. Service: Expose the Deployment internally
apiVersion: v1
kind: Service
metadata:
  name: demo-app-service
spec:
  selector:
    app: demo-app
  ports:
    - port: 80
      targetPort: 80
  type: ClusterIP
```

---

## 4. How the Application Sees This Configuration

Inside the container:

### 4.1 Environment Variables

The pod will have environment variables like:
- `APP_NAME`
- `APP_ENV`
- `LOG_LEVEL`
- `WELCOME_MESSAGE`
- `DB_USERNAME`
- `DB_PASSWORD`
- `APP_NAME_EXPLICIT`
- `DB_USER_EXPLICIT`

### 4.2 Mounted Files

Under `/etc/demo-config` (from ConfigMap):
- `/etc/demo-config/APP_NAME`
- `/etc/demo-config/APP_ENV`
- `/etc/demo-config/LOG_LEVEL`
- `/etc/demo-config/WELCOME_MESSAGE`

Under `/etc/demo-secret` (from Secret):
- `/etc/demo-secret/DB_USERNAME`
- `/etc/demo-secret/DB_PASSWORD`

---

## 5. Best Practices for ConfigMaps & Secrets

- ✅ Store non-sensitive data in **ConfigMaps**
- ✅ Store sensitive data in **Secrets**
- ✅ Do not hardcode secrets in images or code
- ✅ Use `envFrom` for full config load, `env` for fine control
- ✅ Prefer mounting Secrets as files for certificates and keys
- ✅ Use RBAC to restrict access to Secrets
- ✅ Consider enabling **encryption at rest** for Secrets (etcd)
- ✅ Use GitOps (Argo CD / Flux) with sealed or external secrets if possible

---

## 6. Applying and Testing

Apply the full manifest:

```bash
kubectl apply -f demo-config-with-deployment.yaml
```

Check resources:

```bash
kubectl get configmap demo-app-config
kubectl get secret demo-db-secret
kubectl get deployment demo-app-deployment
kubectl get pods
kubectl get svc demo-app-service
```

Inspect environment variables in a pod:

```bash
kubectl exec -it <pod-name> -- env | grep APP_
kubectl exec -it <pod-name> -- env | grep DB_
```

List mounted files:

```bash
kubectl exec -it <pod-name> -- ls /etc/demo-config
kubectl exec -it <pod-name> -- ls /etc/demo-secret
```

---

## 7. Summary

In this document, we covered:

- Detailed behavior of **ConfigMaps** and **Secrets**
- Different ways to use them (env vars & volumes)
- A **single, production-like Deployment** using both
- How to verify configuration from inside the pod
- Best practices for real-world Kubernetes environments



