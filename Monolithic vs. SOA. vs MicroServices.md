
## What is Monolith Architecture?

[Monolithic architecture](https://www.geeksforgeeks.org/monolithic-architecture-system-design/) refers to a single unified codebase where all components of an application are interconnected and interdependent. In this model, the entire application is built as one unit, making it easier to develop and deploy initially.

#### Characteristics of Monolith Architecture:

- ***Single Codebase***: All application components reside within a single codebase, simplifying development and deployment.
- ***Tightly Coupled***: Components are highly interconnected, making changes to one part of the application potentially affect others.
- ***Easier to Test***: Integrated testing can be straightforward, as everything is in one place.
- ***Simpler Deployment***: A single deployment process is required, reducing complexity.

## What is Service-Oriented Architecture (SOA)?

[Service-Oriented Architecture](https://www.geeksforgeeks.org/service-oriented-architecture/) is an architectural pattern that structures an application as a collection of loosely coupled services. Each service represents a specific business function and can be independently developed, deployed, and scaled.

#### Characteristics of SOA:

- ***Loose Coupling***: Services interact through well-defined interfaces, minimizing dependencies between them.
- ***Interoperability***: SOA enables different services to communicate, regardless of the technology stack used.
- ***Reusability***: Services can be reused across different applications, improving development efficiency.
- [***Scalability***](https://www.geeksforgeeks.org/what-is-scalability/): Individual services can be scaled independently based on demand.

## What is Microservices Architecture?

[Microservices architecture](https://www.geeksforgeeks.org/microservices/) is a more granular approach to SOA, where an application is broken down into smaller, independently deployable services. Each microservice focuses on a specific business capability and communicates with others via APIs.

#### Characteristics of Microservices Architecture:

- ***Highly Decoupled***: Microservices are designed to function independently, allowing for isolated development and deployment.
- ***Focused Functionality***: Each microservice serves a specific business capability, enabling teams to work on different features simultaneously.
- ***Continuous Delivery***: Microservices can be deployed independently, enabling faster updates and continuous integration.
## Use Cases of Monolith Architecture

Below are some main use cases of of monolith architecture:

- ***Small Applications***: Ideal for small-scale applications where complexity is low and a quick development cycle is needed.
- ***Startups***: Many startups begin with a monolithic approach to quickly build and validate their product before scaling.
- ***Legacy Systems***: Existing applications that have not transitioned to newer architectures often remain monolithic.

## Use Cases of Service-Oriented Architecture (SOA)

Below are some main use cases of Service-Oriented Architecture (SOA) architecture:

- ***Enterprise Applications***: Large organizations often adopt SOA to integrate various systems and improve interoperability between departments.
- ***Integration Scenarios***: SOA is effective for integrating legacy systems with new applications, allowing for gradual modernization.
- ***Business Process Management***: Companies that require dynamic and adaptable business processes can benefit from SOA's flexibility.

## Use Cases of Microservices Architecture

Below are some main use cases of Microservices Architecture:

- ***E-commerce Platforms***: Companies like Amazon utilize microservices to handle various functions (e.g., inventory, payment) independently, allowing for rapid updates and scalability.
- ***Streaming Services***: Platforms like Netflix leverage microservices to provide scalable and resilient services that can handle millions of users simultaneously.
- ***Continuous Deployment***: Organizations that need to frequently update and deploy features can use microservices to enhance agility and reduce downtime.




![[Pasted image 20250115165322.png]]

![[Pasted image 20250115170025.png]]

A **container** is a lightweight, standalone, and executable software package that includes everything needed to run an application—code, runtime, libraries, and dependencies. Containers are **isolated** from each other and the host operating system, making them portable across environments (e.g., development, testing, production).

A **container** acts as a housing unit for each microservice, allowing the service to operate in its own environment without interference from others. This synergy is what makes containers the go-to solution for deploying microservices architectures.


A **container orchestrator** is a tool that **manages and automates** the deployment, scaling, and operation of containers, ensuring they run smoothly and efficiently.

It helps organize and control a group of containers working together, so you don’t have to do it manually.




### **Basic Concepts of Kubernetes (K8s)**

Kubernetes is a container orchestration platform that automates the deployment, scaling, and management of containerized applications. Below are its core concepts explained simply.
### **Pod**

- The **smallest deployable unit** in Kubernetes.
- A **pod** is a wrapper around one or more containers that share
### **Node**

- A **node** is a machine (physical or virtual) in the cluster that runs the pods.
- Each node has:
    - **Kubelet**: Manages the node.
    - **Container Runtime**: Runs containers (e.g., Docker, containerd).
    - **Kube Proxy**: Handles networking for pods on the node.
### **Cluster**

- A **cluster** is a set of nodes of Kubernetes.
- It consists of:
    - **Master Node (Control Plane)**: Manages the cluster and schedules workloads.
    - **Worker Nodes**: Run the containerized applications (pods).
### **Namespace**

- A **namespace** is like a **folder** in Kubernetes, used to organize resources in a cluster.
- A way to organizer cluster into virtual sub clusters, that may be helpful when different teams share the same k8s cluster
### **Service**

- A **service** exposes pods to the outside world or other pods.
- It provides a stable **IP address** and **DNS name** for pods, even if their instances change.
- Types of services:
    - **ClusterIP**: Internal cluster communication.
    - **NodePort**: External access via a specific port.
    - **LoadBalancer**: External traffic distribution.

### **Replicaset**
- A **ReplicaSet** is a Kubernetes resource used to ensure that a specific number of **pod replicas** are running at all times. It automatically replaces any pod that fails or is deleted to maintain the desired state.

### **Deployment**

- A **deployment** defines how to deploy and manage pods.
- It helps with:
    - Scaling pods up or down.
    - Ensuring the right number of pods are running.
    - Rolling updates, RollBack for seamless app changes.

### **ConfigMap and Secret**

- **ConfigMap**: Stores configuration data (non-sensitive) as key-value pairs.
- **Secret**: Stores sensitive information (e.g., passwords, API keys) securely.
