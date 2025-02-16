# Kubernetes Cheat Sheet

## Retrieving Resources

To get resources like pods, nodes, deployments, or replica sets:
```sh
kubectl get <resource_type>
```
Example:
```sh
kubectl get pods
kubectl get nodes
kubectl get deployments
kubectl get replicasets
```

## Creating a Deployment

To create a deployment:
```sh
kubectl create deployment <name> --image=<imagename>
```
- `<name>`: Name of the deployment
- `<imagename>`: Name of the image (e.g., `nginx`, `mongo`, etc.)

## Logs and Descriptions

To get logs from a pod:
```sh
kubectl logs <podname>
```

To get details or a description of a pod:
```sh
kubectl describe pod <podname>
```

## Accessing a Pod's Terminal

To get terminal access to a container (e.g., MongoDB):
```sh
kubectl exec -it <podname> -- bin/bash
```
Example:
```sh
kubectl exec -it mongodb-64b79776b9-ld4r5 -- bin/bash
```

## Deleting Resources

To delete a deployment:
```sh
kubectl delete deployment <deploymentname>
```

To delete a namespace:
```sh
kubectl delete namespace <namespace_name>
```

## Scaling and Exposing Deployments

To scale a deployment:
```sh
kubectl scale deployment <deployment_name> --replicas=<num_of_replicas>
```

To expose a deployment as a service:
```sh
kubectl expose deployment <deployment_name> --type=<service_type> --port=<service_port>
```

## Configuration Management

To get the current context:
```sh
kubectl config current-context
```

To set a default namespace for the current context:
```sh
kubectl config set-context --current --namespace=<namespace_name>
```

To edit a resource (e.g., deployment, service):
```sh
kubectl edit <resource_type> <resource_name>
```

To view the cluster configuration:
```sh
kubectl config view
```

## Cluster Information

To get events in the cluster:
```sh
kubectl get events
```

To get cluster information:
```sh
kubectl cluster-info
```

## Applying and Fetching Configuration Files

To apply a configuration file:
```sh
kubectl apply -f <config-file.yaml>
```

To fetch the details of a deployment in YAML format:
```sh
kubectl get deployment <name> -o yaml > <filename.yaml>
```

## Service Management

To get details about a service:
```sh
kubectl describe service <service_name>
```

To list all components:
```sh
kubectl get all | grep <name>
```
- `<name>`: Example: `mongo`

To make a service external, set one of the following:
1. `type: LoadBalancer`
2. `nodePort`

To assign an external IP:
```sh
minikube service <service_name>
```

## Ingress Management

To create an ingress resource:
```sh
kubectl apply -f <ingress-resource.yaml>
```

To get details of ingress resources:
```sh
kubectl get ingress
```

To describe an ingress resource:
```sh
kubectl describe ingress <ingress_name>
```

To delete an ingress resource:
```sh
kubectl delete ingress <ingress_name>
```

## Context and Namespace Management

To list all contexts:
```sh
kubectx
```

To switch to a different context:
```sh
kubectx <context_name>
```

To list all namespaces in the current context:
```sh
kubens
```

To switch to a different namespace in the current context:
```sh
kubens <namespace_name>
```

---
This cheat sheet provides commonly used `kubectl` commands for managing Kubernetes clusters efficiently.


Acknowledgements
I have learned this tutorial from the YouTube channel Techworld with Nana. It's a great resource for learning Kubernetes and other DevOps tools.


This cheat sheet provides commonly used kubectl commands for managing Kubernetes clusters efficiently.