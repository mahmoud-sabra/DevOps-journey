 **[Overview | Kubernetes](https://kubernetes.io/docs/concepts/overview/#why-you-need-kubernetes-and-what-can-it-do)**
# Overview

Kubernetes is a portable, extensible, open source platform for managing containerized workloads and services, that facilitates both declarative configuration and automation. It has a large, rapidly growing ecosystem. Kubernetes services, support, and tools are widely available.

The name Kubernetes originates from Greek, meaning helmsman or pilot. K8s as an abbreviation results from counting the eight letters between the "K" and the "s". Google open-sourced the Kubernetes project in 2014. Kubernetes combines [over 15 years of Google's experience](https://kubernetes.io/blog/2015/04/borg-predecessor-to-kubernetes/) running production workloads at scale with best-of-breed ideas and practices from the community.

[Cluster Architecture | Kubernetes](https://kubernetes.io/docs/concepts/architecture/)
# Cluster Architecture

The architectural concepts behind Kubernetes.

A Kubernetes cluster consists of a control plane plus a set of worker machines, called nodes, that run containerized applications. Every cluster needs at least one worker node in order to run Pods.
The worker node(s) host the Pods that are the components of the application workload. The control plane manages the worker nodes and the Pods in the cluster. In production environments, the control plane usually runs across multiple computers and a cluster usually runs multiple nodes, providing fault-tolerance and high availability.

This document outlines the various components you need to have for a complete and working Kubernetes cluster.![[Pasted image 20250108130954.png]]


## WHY?
### 1. **Container Orchestration** 🐳

Containers (e.g., Docker) revolutionized application deployment by enabling lightweight, portable, and consistent environments. However, managing multiple containers manually can be chaotic. Kubernetes automates this by providing.

- **Deployment**: Easily deploy containers across multiple servers.
- **Scaling**: Automatically scale up/down the number of containers based on demand.
- **Load Balancing**: Evenly distribute traffic across containers.
- **Self-Healing**: Restart failed containers automatically.
### 2. **Improved Resource Utilization** ⚙️

Kubernetes optimizes the use of compute resources (CPU, RAM, storage):

- Containers are scheduled to the best-fit nodes based on available resources.
- Resource limits can be defined to prevent one application from hogging resources.

### 3. **Scalability** 📈

Modern applications often need to handle unpredictable loads. Kubernetes:

- **Horizontal Pod Autoscaling (HPA):** Automatically adds or removes containers (pods) based on CPU, memory, or custom metrics.
- Makes scaling seamless across cloud environments or on-premise infrastructure.

### 4. **Portability Across Clouds** ☁️

Kubernetes is cloud-agnostic, allowing applications to run consistently across:

- Public clouds (AWS, Azure, GCP).
- On-premise data centers.
- Hybrid or multi-cloud setups.

This avoids vendor lock-in and ensures flexibility for businesses.

### 5. **Declarative Configuration** 📝

Kubernetes uses YAML or JSON files for defining infrastructure and application deployments. Benefits include:

- **Version Control:** Store configuration files in Git for traceability.
- **Consistency:** Ensure environments (dev, test, prod) are identical.

### 6. **Self-Healing** 🛠️

If an application crashes, Kubernetes ensures availability by:

- Automatically restarting failed containers.
- Rescheduling containers on healthy nodes.
- Rolling back faulty updates.

### Summary: Why Kubernetes is Needed

Without Kubernetes, managing containerized applications in a production environment would be complex, error-prone, and inefficient. Kubernetes provides automation, scalability, and reliability, making it a cornerstone of modern infrastructure.
# Kubernetes Architecture

Kubernetes (K8s) has a robust architecture designed to automate the deployment, scaling, and management of containerized applications. Here’s an overview of its architecture:

---


## 🌟 Core Components of Kubernetes Architecture
[Kubernetes Components | Kubernetes](https://kubernetes.io/docs/concepts/overview/components/)
### 1. Master Node (Control Plane)  
Responsible for managing the cluster and scheduling workloads.  

- ## kube-apiserver [](https://kubernetes.io/docs/concepts/architecture/#kube-apiserver)
  - Acts as the entry point for all administrative tasks.  
  - Validates and processes API requests.  
![[Pasted image 20250111131528.png]]
- ## **Etcd** 
  - Consistent and highly-available key value store used as Kubernetes' backing store for all cluster data.
![[Pasted image 20250111131710.png]]
- ## **Controller Manager**  
  - Manages controllers like the Node Controller, Replication Controller, and others.  
  - Ensures the cluster's desired state matches the actual state.  
![[Pasted image 20250111131840.png]]
![[Pasted image 20250111131915.png]]
- ### kube-scheduler
  -  Control plane component that watches for newly created [Pods](https://kubernetes.io/docs/concepts/workloads/pods/) with no assigned [node](https://kubernetes.io/docs/concepts/architecture/nodes/), and selects a node for them to run on.
  - Assigns workloads (pods) to worker nodes based on resource requirements and constraints.  
  - ![[Pasted image 20250111132025.png]]

---

### 2. Worker Node  
Executes workloads (pods) and reports to the Master Node.  

- **Kubelet**  
  - Communicates with the API Server and ensures that containers are running as specified.  

- **Kube-Proxy**  
  - Manages network rules and facilitates communication between services.  

- **Container Runtime**  
  - Runs containerized applications (e.g., Docker, CRI-O, containerd).  

---
![[Pasted image 20250108130724.png]]

---

 
## API Overview
The REST API is the true keystone of Kubernetes.
Everything within the Kubernetes is as an API Object
### **API Groups**
- **API Groups** organize Kubernetes resources into logical groups (e.g., `core`, `apps`, `batch`) for scalability and modularity.
- The **Core Group** (e.g., Pods, Services) has no group name, while others like `apps` and `batch` are named groups.
- API Groups allow versioning (e.g., `apps/v1`, `apps/v1beta1`) to maintain backward compatibility.
- **Custom Resource Definitions (CRDs)** enable users to create their own API groups for custom functionality.
- Access resources via RESTful endpoints, e.g., `/api/v1/pods` (core) or `/apis/apps/v1/deployments` (apps).

Referenced within an object as the **apiVersion** and **kind**

For exmaple 
```
apiVersion: v1
kind: Pod 
metdata:
spec: 


status:

```

### **Object Model**
Kubernetes uses an **Object Model** to represent the state and configuration of resources within the cluster. These objects are **persistent entities** that describe the desired state of the system, which Kubernetes actively manages to match the actual state.

**Declarative Nature**:

- Users declare the **desired state** in object manifests, and Kubernetes ensures the actual state matches it.
## 🌐 Kubernetes Objects

- **Workloads**: Pod, Deployment, StatefulSet, Job.
- **Networking**: Service, Ingress, NetworkPolicy.
- **Configuration**: ConfigMap, Secret.
- **Storage**: PersistentVolume, PersistentVolumeClaim.

**Essential Fields in Every Object**:

- **`apiVersion`**: Specifies the API group and version (e.g., `apps/v1`).
- **`kind`**: Defines the type of object (e.g., `Pod`, `Service`).
- **`metadata`**: Includes identifying information like `name`, `namespace`, and `labels`.
- **`spec`**: Describes the desired state of the object (e.g., number of replicas).
- **`status`**: Represents the current state of the object (updated by Kubernetes).

### **Object Lifecycle**

1. **Create**: Define the object (e.g., in YAML) and apply it using `kubectl apply`.
2. **Manage**: Kubernetes ensures the desired state is met (e.g., restarting failed Pods).
3. **Update**: Modify the object (e.g., update the image version).
4. **Delete**: Remove the object using `kubectl delete`.
### **Summary in 5 Lines**

1. Kubernetes objects represent the desired state of the cluster.
2. Core fields: `apiVersion`, `kind`, `metadata`, `spec`, `status`.
3. Users define objects declaratively using YAML/JSON manifests.
4. Controllers reconcile the desired state (defined in `spec`) with the actual state (`status`).
5. Example objects: Pod, Deployment, Service, ConfigMap, PersistentVolume.



[Install Tools | Kubernetes](https://kubernetes.io/docs/tasks/tools/)

## **Minikube** [minikube start | minikube](https://minikube.sigs.k8s.io/docs/start/?arch=%2Flinux%2Fx86-64%2Fstable%2Fbinary+download)

minikube is local Kubernetes, focusing on making it easy to learn and develop for Kubernetes.

All you need is Docker (or similarly compatible) container or a Virtual Machine environment, and Kubernetes is a single command away: `minikube start`

---

----
![[Pasted image 20250115171130.png]]

-----
### **What are Labels?**

- **Labels** are **key-value pairs** attached to Kubernetes objects (like Pods, Services, ReplicaSets, etc.).
- They help organize, categorize, and identify resources.
- Labels are **customizable**, meaning you can define them as per your needs.
```
metadata:
  labels:
	name: app1
    app: frontend
    environment: production
    version: v1

```
### **What are Selectors?**

- **Selectors** are used to **find and match** Kubernetes objects based on their labels.
- They define a **filtering mechanism** to group objects for operations like scaling or exposing services.
```
spec:
  selector:
    matchLabels:
      app: frontend
      environment: production
      
```
![[Pasted image 20250115201835.png]]

```
apiVersion: v1
kind: Pod
metadata:
  name: nginx-pod
  labels:
    app: nginx
spec:
  containers:
  - name: nginx-container
    image: nginx:latest
    ports:
    - containerPort: 80

```

ReplicaSet 
```
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: nginx-replicaset
spec:
  replicas: 3  # Number of replicas
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx-container
        image: nginx:latest
        ports:
        - containerPort: 80

```
Deployment
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  replicas: 3  # Number of replicas
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx-container
        image: nginx:1.21  # Specific version of Nginx
        ports:
        - containerPort: 80

```

---- 
How To Know apiVersion?
```
k api-resources
```


![[Pasted image 20250118190651.png]]





### Deployment Strategies in Kubernetes 

Kubernetes provides various deployment strategies to roll out updates to applications with minimal downtime and controlled impact. These strategies help ensure smooth updates, efficient resource usage, and reduced risk.

### 1. **Recreate Strategy**

The **Recreate** strategy shuts down all existing Pods and then creates new ones.

#### How It Works:

- All existing Pods are terminated.
- New Pods are started with the updated configuration.

#### Use Case:

- Best for **stateless** applications or when downtime is acceptable.
- Suitable when the new version is incompatible with the old version.
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: example-deployment
spec:
  replicas: 3
  strategy:
    type: Recreate
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
      - name: nginx
        image: nginx

```

### 2. **RollingUpdate Strategy** (Default)

The **RollingUpdate** strategy replaces old Pods incrementally with new ones to minimize downtime.

#### How It Works:

- A new Pod is created before deleting an old one (controlled by `maxSurge` and `maxUnavailable`).
- Ensures some Pods are always available during the update.

#### Parameters:

- `maxUnavailable`: The maximum number of Pods that can be unavailable during the update.
- `maxSurge`: The maximum number of extra Pods that can be created during the update.

#### Use Case:

- Best for applications requiring **high availability**.
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: example-deployment
spec:
  replicas: 3
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxUnavailable: 1
      maxSurge: 1
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
      - name: nginx
        image: nginx

```

### **Blue/Green Deployment**

In this strategy, two separate environments (blue and green) are maintained. One serves live traffic (blue), while the other (green) runs the new version.

#### How It Works:

- Deploy the new version to the green environment.
- Perform testing and validation.
- Switch live traffic to the green environment.

#### Use Case:

- Applications requiring **zero downtime** and thorough validation before release.
- Often managed externally (e.g., using load balancers or service mesh tools).

#### Implementation:

- Not directly supported in Kubernetes but can be achieved using **Services** and labels.
```
apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  selector:
    app: my-app-blue
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: blue-deployment
spec:
  replicas: 3
  template:
    metadata:
      labels:
        app: my-app-blue
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: green-deployment
spec:
  replicas: 3
  template:
    metadata:
      labels:
        app: my-app-green

```


Create Two Deployment prod and dev with image nginx, label them  env=prod for the first one and other env=dev, make sure the Prod deployment in namespace called prod  and the  the dev in namespace dev, try to show lables

in dev deployment use the strategy recreate and in prod deployment use the default startegy
change the image of both deployment to nginx:mainline-perl

------------------------

Conofigmap
```
apiVersion: v1
kind: ConfigMap
metadata:
  name: my-configmap
data:
  MYVAR: "isAwesome"

```

```
apiVersion: v1
kind: Pod
metadata:
  name: nginx-override-cmd
spec:
  containers:
  - name: nginx
    image: nginx
    ports:
    - containerPort: 80
      name: http
      protocol: TCP
    env:
    - name: MYVAR
      valueFrom:
        configMapKeyRef:
          name: my-configmap
          key: MYVAR
    command:
    - "/bin/sh"
    - "-c"
    args:
    - "echo ${MYVAR}"

```



### **What are Kubernetes Secrets?** 🛡️

Kubernetes **Secrets** are objects designed to store and manage sensitive information, such as passwords, OAuth tokens, SSH keys, or API keys, securely. They help keep sensitive data separate from application code, reducing the risk of accidental exposure.

### **Types of Secrets**

1. **Opaque** (default): General-purpose key-value pairs.
2. **Service Account Token**: Automatically created for Pods to access the API.
3. **Docker Registry Secret**: Stores credentials for accessing private Docker registries.
4. **TLS Secret**: Contains TLS certificates and private keys for HTTPS.
5. **Basic Authentication Secret**: Stores `username` and `password` for basic authentication

**Base64 Encoding**: Secrets store data encoded in Base64 for easy handling, though they are not encrypted by default.
```
apiVersion: v1
kind: Secret
metadata:
  name: my-secret
type: Opaque
data:
  MYVAR: aXNBd2Vzb21l # Base64 encoded value of "isAwesome"

```

```
kubectl create secret generic my-secret \
  --from-literal=MYVAR=isAwesome

```

```
apiVersion: v1
kind: Pod
metadata:
  name: nginx-override-cmd
spec:
  containers:
  - name: nginx
    image: nginx
    ports:
    - containerPort: 80
      name: http
      protocol: TCP
    env:
    - name: MYVAR
      valueFrom:
        secretKeyRef:
          name: my-secret
          key: MYVAR
    command:
    - "/bin/sh"
    - "-c"
    args:
    - "echo ${MYVAR}"

```
In Kubernetes, **Services** provide a stable networking endpoint for accessing Pods. Since Pods are ephemeral and can be replaced frequently, Services abstract the Pod's lifecycle, ensuring consistent access.

### **Why Do We Need Services?**

1. Pods have dynamic IPs that change when Pods are recreated.
2. Services provide a consistent way to access Pods regardless of their IP changes.
3. They enable load balancing and expose applications to internal/external traffic.

### **Types of Services**

1. **ClusterIP** (Default)
    
    - Exposes the Service internally within the cluster.
    - No external access.
    ![[Pasted image 20250125142555.png]]
1. **NodePort**
    
    - Exposes the Service on each node's IP and a static port.
    - Allows external access to the cluster.
    ![[Pasted image 20250125142609.png]]
1. **LoadBalancer**
    
    - Exposes the Service externally using a cloud provider's load balancer.
    - Common in cloud environments.
    ![[Pasted image 20250125142658.png]]
1. **ExternalName**
    
    - Maps a Service to an external DNS name.

```
apiVersion: v1
kind: Pod
metadata:
  name: nginx-pod
  labels:
    app: nginx
    env: prod
spec:
  containers:
  - name: nginx-container
    image: nginx:latest
    ports:
    - containerPort: 80

```

ClusterIP
```
apiVersion: v1
kind: Service
metadata:
  name: example-prod
spec:
  type: ClusterIP
  selector:
    app: nginx
    env: prod
  ports:
    protocol: TCP
    port: 80
    targetPort: 80
```

- NodePort services extend the ClusterIP service.
- Exposes a port on everynode’s IP.
- Port can either be statically defined, or dynamically taken from a range between 30000-32767.
```
apiVersion: v1
kind: Service
metadata:
  name: example-prod
spec:
  type: NodePort
  selector:
    app: nginx
    env: prod
  ports:
  - nodePort: 32410
    protocol: TCP
    port: 80
    targetPort: 80

```

Loadbalancer 
```
apiVersion: v1
kind: Service
metadata:
  name: backend-service
spec:
  type: LoadBalancer
  selector:
    app: backend
  ports:
  - protocol: TCP
    port: 80
    targetPort: 80

```

-----
Volumes:
**Container Ephemeral Nature**: Containers lose data when they restart. Kubernetes Volumes address this issue by:

1. Providing storage that persists beyond container restarts.
2. Sharing data between multiple containers in a Pod.

Volumes are **directories with data**, accessible to containers in a Pod. They are mounted inside the containers and abstract different storage backends like host disks, cloud storage, or network storage.

Anatomy of a Kubernetes Volume:
- **`volumes`** (defined in the Pod spec):
    - Specifies the type and source of the volume.
- **`volumeMounts`** (inside containers):
    - Specifies where the volume should be mounted inside the container.
    

```
apiVersion: v1
kind: Pod
metadata:
  name: volume-example
spec:
  containers:
  - name: nginx-content
    image: nginx:stable-alpine
    volumeMounts:
    - name: html
      mountPath: /usr/share/nginx/html
  volumes:
  - name: html
    emptyDir: {}

```

```
k exec volume-example -it -c nginx-content -- /bin/sh

```

```
apiVersion: v1
kind: Pod
metadata:
  name: volume-example2
spec:
  containers:
  - name: nginx
    image: nginx:stable-alpine
    volumeMounts:
    - name: html
      mountPath: /usr/share/nginx/html
  - name: content
    image: alpine:latest
    command: ["/bin/sh", "-c"]
    args: ["while true; do date >> /html/index.html; sleep 5; done"]
    volumeMounts:
    - name: html
      mountPath: /html
  volumes:
  - name: html
    emptyDir: {}

```


![[Pasted image 20250125151314.png]]

![[Pasted image 20250125151447.png]]![[Pasted image 20250125151605.png]]![[Pasted image 20250125154443.png]]![[Pasted image 20250125154804.png]]

```
apiVersion: v1
kind: PersistentVolume
metadata:
  name: pv-example
spec:
  capacity:
    storage: 5Gi
  accessModes:
    - ReadWriteOnce
  hostPath:
    path: /mnt/data

```

```
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: pvc-example
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 5Gi

```


![[Pasted image 20250201151441.png]]
```
---
apiVersion: apps/v1
kind: DaemonSet
metadata:
  labels:
    app: elasticsearch
  name: elasticsearch
  namespace: kube-system
spec:
  selector:
    matchLabels:
      app: elasticsearch
  template:
    metadata:
      labels:
        app: elasticsearch
    spec:
      containers:
      - image: nginx
        name: fluentd-elasticsearch
```

StatefulSet
A **StatefulSet** is used to **manage stateful applications** in Kubernetes Like database
```
apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: nginx
spec:
  selector:
    matchLabels:
      app: nginx
  serviceName: "nginx"
  replicas: 3
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
        - name: nginx
          image: nginx:latest
          ports:
            - containerPort: 80
              name: http

```
Job

A **Job** in Kubernetes is a resource used to **run a one-time task** to completion. It ensures that the specified task or process runs **successfully** to its end, even if the pods fail or the task needs to be retried.
### **Use Cases of Jobs**

✔️ **Batch processing** (e.g., process files and exit).  
✔️ **Data migrations** (e.g., schema changes in a database).  
✔️ **One-time tasks** (e.g., backups, cleanup).
```
apiVersion: batch/v1
kind: Job
metadata:
  name: test-job
spec:
  completions: 1  # Run the job once
  parallelism: 1  # Run one pod at a time
  template:
    spec:
      restartPolicy: Never
      containers:
        - name: busybox
          image: busybox
          command: ["echo", "Hello from Kubernetes Job!"]

```
CronJob

A **CronJob** in Kubernetes is a **controller** that **creates Jobs** on a schedule. Each time the CronJob runs, it runs a new Job**, which then runs a pod to execute the task.
```
apiVersion: batch/v1
kind: CronJob
metadata:
  name: test-cronjob
spec:
  schedule: "*/1 * * * *"  # Runs every 1 minute
  jobTemplate:
    spec:
      template:
        spec:
          restartPolicy: Never
          containers:
            - name: busybox
              image: busybox
              command: ["echo", "Hello from Kubernetes CronJob!"]

```
### **Use Cases of CronJobs**
- **Scheduled Backups**: Automate regular backups of databases or files.
- **Log Rotation**: Clean up logs or rotate files at defined intervals.
- **Data Synchronization**: Sync data between systems periodically.