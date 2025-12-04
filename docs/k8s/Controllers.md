---
sidebar_position: 8
---

# Kubernetes Controllers

This document explains the **main Kubernetes controllers**, why they are used, how they work,
and provides **YAML examples** for each, along with **comparison tables**.

Controllers covered:

- ReplicationController (legacy)
- ReplicaSet
- Deployment
- StatefulSet
- DaemonSet
- Job
- CronJob

---

## 1. What is a Kubernetes Controller?

A **Kubernetes controller** is a control loop that:
- Observes the **current state** of the cluster (from the API server)
- Compares it with the **desired state** (from your YAML manifests)
- Takes actions to **reconcile differences automatically**

> You declare *what you want*, controllers ensure it stays that way.

Example desired state:
```yaml
replicas: 3
```
If only 2 Pods are running, the controller creates 1 more Pod.

---

## 2. ReplicationController (Legacy)

### 2.1 What is a ReplicationController?

A **ReplicationController (RC)** ensures that a specified number of Pod replicas are always running.

> It is an **older controller**, mostly replaced by **ReplicaSet** and **Deployment**.

### 2.2 When is it used?

- Only in **older clusters** or legacy manifests.
- Not recommended for new deployments.

### 2.3 Basic YAML Example – ReplicationController

```yaml
apiVersion: v1
kind: ReplicationController
metadata:
  name: nginx-rc
spec:
  replicas: 2
  selector:
    app: nginx-rc
  template:
    metadata:
      labels:
        app: nginx-rc
    spec:
      containers:
        - name: nginx
          image: nginx:1.25
          ports:
            - containerPort: 80
```

---

## 3. ReplicaSet

### 3.1 What is a ReplicaSet?

A **ReplicaSet** is the modern replacement for ReplicationController.
It ensures that a **specified number of identical Pods** are always running.

> It is usually **managed by a Deployment**, not created directly.

### 3.2 When is it used?

- Rarely used directly.
- Mainly created and managed by **Deployment** objects.

### 3.3 Basic YAML Example – ReplicaSet

```yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: nginx-rs
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx-rs
  template:
    metadata:
      labels:
        app: nginx-rs
    spec:
      containers:
        - name: nginx
          image: nginx:1.25
          ports:
            - containerPort: 80
```

---

## 4. Deployment

### 4.1 What is a Deployment?

A **Deployment** is the most commonly used controller for **stateless applications**.

It manages:
- ReplicaSets
- Rolling updates
- Rollbacks
- Scaling

> Deployment is the **standard way** to run stateless workloads in Kubernetes.

### 4.2 When is it used?

- Web apps
- REST APIs
- Microservices
- Any stateless service

### 4.3 Basic YAML Example – Deployment

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  replicas: 2
  selector:
    matchLabels:
      app: nginx-app
  template:
    metadata:
      labels:
        app: nginx-app
    spec:
      containers:
        - name: nginx
          image: nginx:1.25
          ports:
            - containerPort: 80
```

### 4.4 Key Features

- Rolling updates (zero downtime)
- Easy rollback
- Horizontal scaling
- Versioned ReplicaSets

---

## 5. StatefulSet

### 5.1 What is a StatefulSet?

A **StatefulSet** is a controller designed for **stateful applications** that need:

- Stable network identity
- Stable persistent storage
- Ordered deployment & termination

> Each Pod in a StatefulSet has a **sticky identity** (name/index).

Example pod names:
- `mysql-0`
- `mysql-1`
- `mysql-2`

### 5.2 When is it used?

- Databases (MySQL, PostgreSQL, MongoDB)
- Distributed systems (Kafka, Zookeeper, Cassandra)
- Apps requiring persistent identity

### 5.3 Basic YAML Example – StatefulSet

```yaml
apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: web-stateful
spec:
  serviceName: "web"
  replicas: 3
  selector:
    matchLabels:
      app: web
  template:
    metadata:
      labels:
        app: web
    spec:
      containers:
        - name: nginx
          image: nginx:1.25
          ports:
            - containerPort: 80
  volumeClaimTemplates:
    - metadata:
        name: web-data
      spec:
        accessModes: ["ReadWriteOnce"]
        resources:
          requests:
            storage: 1Gi
```

### 5.4 Key Features

- Stable pod names
- Per-pod storage (PVC per pod)
- Ordered, graceful rollout and termination

---

## 6. DaemonSet

### 6.1 What is a DaemonSet?

A **DaemonSet** ensures that **one Pod runs on each (or selected) node**.

> Ideal for cluster-wide agents that must run everywhere.

### 6.2 When is it used?

- Logging agents (Fluentd, Filebeat)
- Monitoring agents (Node Exporter)
- Network plugins (CNI)
- Security agents

### 6.3 Basic YAML Example – DaemonSet

```yaml
apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: node-logger
spec:
  selector:
    matchLabels:
      app: node-logger
  template:
    metadata:
      labels:
        app: node-logger
    spec:
      containers:
        - name: logger
          image: busybox:1.36
          command:
            - sh
            - -c
            - "while true; do echo Logging from $(hostname); sleep 10; done"
```

### 6.4 Key Features

- One pod per node (or per matching node)
- Automatically handles new nodes joining the cluster

---

## 7. Job

### 7.1 What is a Job?

A **Job** runs a **task to completion**.

> Use Job when you need **one-off or batch tasks** that **must finish**, not run forever.

### 7.2 When is it used?

- Batch processing
- Data migration
- Database cleanup
- Report generation

### 7.3 Basic YAML Example – Job

```yaml
apiVersion: batch/v1
kind: Job
metadata:
  name: pi-calculation
spec:
  template:
    metadata:
      name: pi-job
    spec:
      restartPolicy: Never
      containers:
        - name: pi
          image: perl
          command: ["perl", "-Mbignum=bpi", "-wle", "print bpi(50)"]
  backoffLimit: 3
```

### 7.4 Key Features

- Ensures the task runs to completion
- Retries on failure (up to `backoffLimit`)

---

## 8. CronJob

### 8.1 What is a CronJob?

A **CronJob** runs a Job **on a schedule**, similar to Linux `cron`.

> Use CronJob for **recurring tasks**.

### 8.2 When is it used?

- Nightly backups
- Regular cleanup jobs
- Scheduled reports
- Periodic sync tasks

### 8.3 Basic YAML Example – CronJob

```yaml
apiVersion: batch/v1
kind: CronJob
metadata:
  name: nightly-backup
spec:
  schedule: "0 2 * * *"   # Every day at 2:00 AM
  jobTemplate:
    spec:
      template:
        spec:
          restartPolicy: OnFailure
          containers:
            - name: backup
              image: busybox:1.36
              command:
                - sh
                - -c
                - "echo Running backup... && sleep 30 && echo Backup completed."
```

### 8.4 Key Features

- Time-based scheduling
- Creates Jobs as per schedule
- Can limit history of successful/failed jobs

---

## 9. Controller Comparison Table

### 9.1 Workload Controllers Summary

| Controller          | Primary Use Case              | Pod Identity | Storage Behavior      | Run Mode          |
|---------------------|-------------------------------|-------------|-----------------------|-------------------|
| ReplicationController | Legacy replica management  | Stateless   | No special handling   | Long-running      |
| ReplicaSet          | Maintain Pod replicas         | Stateless   | No special handling   | Long-running      |
| Deployment          | Stateless apps, rolling updates | Stateless | No special handling   | Long-running      |
| StatefulSet         | Stateful apps, databases      | Stateful    | Per-pod persistent PVC | Long-running     |
| DaemonSet           | Node-level agents             | Per node    | Optional              | Long-running      |
| Job                 | One-off tasks                 | N/A         | Optional              | Run-to-completion |
| CronJob             | Scheduled jobs                | N/A         | Optional              | Run-to-completion (repeated) |

---

### 9.2 Deployment vs StatefulSet vs DaemonSet

| Feature                | Deployment         | StatefulSet           | DaemonSet               |
|------------------------|-------------------|-----------------------|-------------------------|
| For stateless apps     | ✅ Yes            | ❌ Usually not        | ❌ No                   |
| For stateful apps      | ❌ No             | ✅ Yes                | ❌ No                   |
| Stable Pod names       | ❌ No             | ✅ Yes                | ❌ No                   |
| Per-pod storage        | ❌ No             | ✅ Yes (PVC)          | Optional                |
| One Pod per node       | ❌ No             | ❌ No                 | ✅ Yes                  |
| Rolling updates        | ✅ Yes            | ✅ Yes (ordered)      | ✅ Yes                  |

---

### 9.3 Job vs CronJob

| Feature            | Job                        | CronJob                         |
|--------------------|----------------------------|---------------------------------|
| Execution          | One-time                   | Repeated on schedule            |
| Use case           | Batch task                 | Recurring batch task            |
| Created resource   | Pod(s)                     | Job (which then runs Pods)      |
| Example            | Data import                | Nightly backup                  |

---

## 10. Summary

- Controllers are the **automation brain** of Kubernetes.
- They continuously work to maintain the **desired state**.
- Different controllers are used for:
  - Stateless apps → **Deployment**
  - Stateful apps → **StatefulSet**
  - Node-wide agents → **DaemonSet**
  - Batch jobs → **Job**
  - Scheduled jobs → **CronJob**
- ReplicationController and ReplicaSet are **lower-level**, while Deployment, StatefulSet, DaemonSet, Job, and CronJob are **higher-level, real-world controllers**.

Understanding these controllers is **essential for building and operating real Kubernetes workloads**.

## Comparison: Stateless vs Stateful Controllers

### Conceptual Difference

| Aspect                 | Stateless Controller (Deployment)           | Stateful Controller (StatefulSet)                  |
|------------------------|---------------------------------------------|---------------------------------------------------|
| Pod Identity           | Not important                              | Very important                                    |
| Pod Names              | Random (e.g., `nginx-abc123`)              | Stable (e.g., `mysql-0`, `mysql-1`)               |
| Storage                | Usually shared or external                 | Per-pod persistent volume                         |
| Scaling Safety         | Easy and safe                              | Requires careful scaling (data-aware)             |
| Use Case               | Web apps, APIs, frontends                  | Databases, queues, distributed systems            |
| Rollout Behavior       | Non-ordered                                | Ordered (if needed)                               |
| Pod Replacement        | Any Pod can be deleted & recreated         | Pods may hold unique data                         |
