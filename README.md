# Kubernetes Commands Reference Guide

## Table of Contents
1. [Cluster Information](#cluster-information)
2. [Resource Management](#resource-management)
3. [Pod Operations](#pod-operations)
4. [Deployment Operations](#deployment-operations)
5. [Service Operations](#service-operations)
6. [Namespace Operations](#namespace-operations)
7. [ConfigMap and Secrets](#configmap-and-secrets)
8. [Logging and Debugging](#logging-and-debugging)
9. [Port Forwarding](#port-forwarding)
10. [Context and Configuration](#context-and-configuration)

## Cluster Information
```bash
# Get cluster information
kubectl cluster-info

# Check API versions supported
kubectl api-versions

# View kubectl configuration
kubectl config view

# Check component status
kubectl get componentstatuses

# Get nodes information
kubectl get nodes
kubectl describe node <node-name>
```

## Resource Management
```bash
# Get all resources in current namespace
kubectl get all

# Get all resources in all namespaces
kubectl get all --all-namespaces
kubectl get all -A

# Get specific resource types
kubectl get pods,svc,deployments
kubectl get <resource-type> --show-labels

# Watch resources in real-time
kubectl get <resource-type> -w

# Get detailed information about a resource
kubectl describe <resource-type> <resource-name>
```

## Pod Operations
```bash
# List pods
kubectl get pods
kubectl get pods -o wide
kubectl get pods --field-selector=status.phase=Running

# Create pod from file
kubectl create -f pod.yaml

# Delete pod
kubectl delete pod <pod-name>
kubectl delete pod <pod-name> --force --grace-period=0

# Execute command in pod
kubectl exec -it <pod-name> -- /bin/bash
kubectl exec <pod-name> -- <command>

# Copy files to/from pod
kubectl cp <pod-name>:/path/to/file local-file
kubectl cp local-file <pod-name>:/path/to/file
```

## Deployment Operations
```bash
# Create and manage deployments
kubectl create deployment <name> --image=<image>
kubectl scale deployment <name> --replicas=<number>
kubectl rollout status deployment/<name>

# Update deployment
kubectl set image deployment/<name> <container>=<image>
kubectl rollout history deployment/<name>
kubectl rollout undo deployment/<name>

# Edit deployment
kubectl edit deployment <name>

# Delete deployment
kubectl delete deployment <name>
```

## Service Operations
```bash
# List services
kubectl get services
kubectl get svc

# Create service
kubectl expose deployment <name> --port=<port> --target-port=<target-port>
kubectl create service clusterip <name> --tcp=<port>:<target-port>

# Delete service
kubectl delete service <name>
```

## Namespace Operations
```bash
# List namespaces
kubectl get namespaces
kubectl get ns

# Create namespace
kubectl create namespace <name>

# Set default namespace
kubectl config set-context --current --namespace=<name>

# Delete namespace
kubectl delete namespace <name>
```

## ConfigMap and Secrets
```bash
# ConfigMap operations
kubectl create configmap <name> --from-file=<path>
kubectl create configmap <name> --from-literal=key=value
kubectl get configmaps
kubectl describe configmap <name>

# Secret operations
kubectl create secret generic <name> --from-literal=key=value
kubectl get secrets
kubectl describe secret <name>
```

## Logging and Debugging
```bash
# View pod logs
kubectl logs <pod-name>
kubectl logs <pod-name> -c <container-name>
kubectl logs -f <pod-name>  # Follow logs
kubectl logs --tail=100 <pod-name>  # Last 100 lines

# Debugging
kubectl describe pod <pod-name>
kubectl get events
kubectl top pods  # Resource usage
kubectl top nodes
```

## Port Forwarding
```bash
# Forward port from pod
kubectl port-forward <pod-name> <local-port>:<pod-port>

# Forward port from service
kubectl port-forward service/<service-name> <local-port>:<service-port>

# Forward with specific address binding
kubectl port-forward --address 0.0.0.0 <pod-name> <local-port>:<pod-port>
```

## Context and Configuration
```bash
# View and manage contexts
kubectl config get-contexts
kubectl config use-context <context-name>
kubectl config current-context

# Set cluster
kubectl config set-cluster <cluster-name> --server=<server-url>

# Set credentials
kubectl config set-credentials <user-name> --token=<bearer-token>

# Set context
kubectl config set-context <context-name> --cluster=<cluster-name> --user=<user-name>
```

## Tips and Best Practices
1. Use `-o wide` for additional information in output
2. Use `--dry-run=client -o yaml` to generate resource YAML
3. Use labels and selectors for better resource management
4. Always specify namespace when working in large clusters
5. Use `kubectl explain <resource>` for resource documentation

## Common Flags and Options
```bash
-n, --namespace           # Specify namespace
-o, --output             # Output format (yaml, json, wide, etc.)
-l, --selector           # Label selector
-A, --all-namespaces     # All namespaces
-f, --filename           # Specify resource file
--force                  # Force operation
--dry-run=client        # Simulate operation
```