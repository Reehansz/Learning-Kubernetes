# Kubernetes (K8s) - A Beginner-Friendly Guide

## 1. Introduction to Kubernetes
Kubernetes (often abbreviated as K8s) is an open-source platform designed to automate the deployment, scaling, and management of containerized applications. It helps ensure that applications run smoothly without manual intervention.

### Why is Kubernetes Needed?
- Manages applications that run in containers (such as Docker).
- Ensures applications are always available and can handle heavy loads.
- Automates scaling, updating, and self-healing of applications.
- Works across different environments (Cloud, On-Premises, Hybrid).

## 2. Kubernetes Architecture - Key Components
Kubernetes is structured in a Master-Worker architecture. Let’s break it down:

### A. Master Node (Control Plane)
This is the brain of Kubernetes, managing everything inside the cluster.

#### Components in Master Node:
- **API Server**: The front door of Kubernetes; all requests (from users or tools like kubectl) go through this.
- **Controller Manager**: Ensures that the system maintains the desired state (e.g., restarts a crashed application).
- **Scheduler**: Decides which worker node should run a new application (pod).
- **etcd**: A distributed database that stores all cluster data (state, configurations, etc.).

#### What does the Master Node do?
- Manages the cluster
- Assigns workloads to worker nodes
- Keeps track of all running applications

### B. Worker Nodes (Where Apps Run)
The worker nodes execute the actual applications. They are controlled by the master node.

#### Components in Worker Nodes:
- **Kubelet**: The manager of the node; ensures that the assigned application (pod) is running properly.
- **Container Runtime**: The software that runs containers (e.g., Docker or containerd).
- **Kube Proxy**: Manages networking, ensuring that services communicate properly.

#### What do Worker Nodes do?
- Run applications inside containers
- Communicate with the master node
- Ensure applications stay up and running

## 3. How Kubernetes Works? (The Lifecycle of an Application)
1. A user creates an application definition (YAML file).
2. The API Server receives the request.
3. The Scheduler decides which worker node will run the application.
4. The Worker Node pulls the container image and starts the app inside a Pod.
5. Kubernetes continuously monitors the application’s health.

## 4. Kubernetes Key Concepts & Terms
- **Pod**: The smallest unit in Kubernetes. It runs one or more containers.
- **Service**: Makes an application accessible across the cluster.
- **Deployment**: Defines how an app should run (e.g., how many copies, update strategies, etc.).
- **Namespace**: A way to divide the cluster into separate environments (e.g., dev, test, prod).
- **Volume**: A directory accessible to containers in a Pod. Allows data to persist across container restarts.
- **StatefulSet**: Manages the deployment and scaling of a set of Pods with unique identities.
- **Secret**: Used to store and manage sensitive information, such as passwords, OAuth tokens, and ssh keys.
- **ConfigMap**: Used to store non-confidential data in key-value pairs.
- **Ingress**: Manages external access to services in a cluster, typically HTTP.
- **DaemonSet**: Ensures that all (or some) nodes run a copy of a Pod.
- **Job**: Creates one or more Pods and ensures that a specified number of them successfully terminate.
- **CronJob**: Manages time-based Jobs, similar to cron in Unix/Linux.
- **ReplicaSet**: Ensures a specified number of Pod replicas are running at any given time.
- **Horizontal Pod Autoscaler**: Automatically scales the number of Pods in a deployment based on observed CPU utilization or other metrics.
- **Persistent Volume**: Abstract storage resources and allow dynamic provisioning of storage.
- **Persistent Volume Claim**: A request for storage by a user.
- **Network Policy**: Defines rules for how Pods communicate with each other and other network endpoints.

## 5. Minikube – A Local Kubernetes Playground
Minikube is a lightweight version of Kubernetes that lets you run a single-node cluster on your own computer. It is great for learning and testing Kubernetes before deploying it in production.

### Why use Minikube?
- Run Kubernetes on a laptop/PC
- Test deployments locally
- Learn Kubernetes without cloud costs

### How to install Minikube?
1. Download Minikube from the official site.
2. Run: `minikube start` to create a Kubernetes cluster.

## 6. kubectl – The Command-Line Tool for Kubernetes
kubectl is the main tool to interact with Kubernetes. It communicates with the API server and helps manage the cluster.

### Common kubectl Commands:
- `kubectl apply -f app.yaml`: Updates an application.
- `kubectl expose deployment <deployment-name> --type=NodePort`: Makes an app accessible externally.

## 7. Summary – What You Should Remember
- Kubernetes is a system that manages containerized applications.
- It has a Master-Worker architecture.
- Master Node manages everything, while Worker Nodes run applications.
- Kubernetes ensures scalability, high availability, and automation.
- Minikube is used for running Kubernetes locally.
- kubectl is the tool used to interact with Kubernetes.


### Layers of Abstractions in Kubernetes
- **Deployment**: Manages the deployment of ReplicaSets and ensures the desired number of Pods are running. It provides declarative updates to applications.
- **ReplicaSet**: Ensures a specified number of Pod replicas are running at any given time. It maintains the desired number of Pods through scaling and self-healing.
- **Pod**: The smallest and simplest Kubernetes object. It represents a single instance of a running process in a cluster and can contain one or more containers.
- **Container**: The actual application or service running inside a Pod. Containers are lightweight and portable executable units that include the application code, runtime, libraries, and dependencies.

This guide should give a clear foundational understanding of Kubernetes for both technical and non-technical readers. 🚀

## Structure of a Kubernetes YAML File

## apiVersion
- Specifies the version of the Kubernetes API to use for this resource.
- Example: `apiVersion: apps/v1`

## kind
- Specifies the type of Kubernetes resource being defined.
- Examples: `Deployment`, `Service`, `Pod`, `ConfigMap`

## metadata
- Contains metadata about the resource, such as its name, namespace, labels, and annotations.
- Example:
  ```yaml
  metadata:
    name: nginx-deployment
    namespace: default
    labels:
      app: nginx
## spec
Defines the desired state of the resource. The content of this section varies depending on the resource type.
Example for a Deployment:
```yaml
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
        image: nginx:1.14.2
        ports:
        - containerPort: 80

## status
Provides the current status of the resource. This section is typically populated by the Kubernetes system and is not included in the initial YAML file.
Example:
```yaml
status:
  replicas: 3
  updatedReplicas: 3
  readyReplicas: 3

## Additional Components
labels
Key-value pairs used to organize and select resources.
Example:
```yaml
metadata:
  labels:
    app: nginx

annotations
Key-value pairs used to attach arbitrary non-identifying metadata to resources.
Example:
```yaml
metadata:
  annotations:
    description: "This is an annotation"

selector
Used to select a group of resources based on their labels.
Example:
```yaml
spec:
  selector:
    matchLabels:
      app: nginx

template
Defines the Pod template for resources like Deployments and ReplicaSets. It includes metadata and spec for the Pods.
Example:
```yaml
template:
  metadata:
    labels:
      app: nginx
  spec:
    containers:
    - name: nginx
      image: nginx:1.14.2
      ports:
      - containerPort: 80

## A Quick review
Sure! In a Kubernetes deployment or service YAML file, there are several sections that define different aspects of the deployment or service. Here's a breakdown of each section:

apiVersion: This section specifies the version of the Kubernetes API that the file is using. It is typically set to "apps/v1" for deployments and "v1" for services.

kind: This section specifies the type of Kubernetes resource that the file is defining. It is typically set to "Deployment" for deployments and "Service" for services.

metadata: This section contains metadata about the deployment or service, such as its name, labels, and annotations.

spec: This section contains the specifications for the deployment or service, such as the number of replicas, the container image, and the ports that the service should listen on.

Here's an example of a deployment YAML file:
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-app
spec:
  replicas: 3
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
      - name: my-app
        image: my-app:latest
        ports:
        - containerPort: 80

In this example, the deployment is named "my-app" and has three replicas. The selector matches pods with the label "app: my-app". The template specifies the container image for the deployment, which is "my-app:latest" and exposes port 80.

Here's an example of a service YAML file:

```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-app
spec:
  selector:
    app: my-app
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
      
In this example, the service is named "my-app" and selects pods with the label "app: my-app". It exposes port 80 on the service and forwards traffic to port 80 on the pods.





