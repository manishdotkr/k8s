# Kubernetes Nginx Deployment on Minikube

## Task: Deploy an Nginx container and access it via the browser

### Platform: Minikube

### Prerequisites
- Install Minikube: [Minikube Installation Guide](https://minikube.sigs.k8s.io/docs/start/?arch=%2Flinux%2Fx86-64%2Fstable%2Fbinary+download)

### Setup Minikube

1. Install Minikube on Linux:
   ```bash
   curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
   sudo install minikube-linux-amd64 /usr/local/bin/minikube
   rm minikube-linux-amd64
   ```

2. Start and interact with Minikube:
   ```bash
   minikube start       # Start Minikube
   minikube status      # Check Minikube status
   minikube dashboard   # Access Minikube dashboard in the browser
   minikube ip          # Get Minikube Ip
   ```

### Common `kubectl` Commands

- List resources (e.g., `pods`, `deployments`, `svc`, `ingress`, `namespaces`):
  ```bash
  kubectl get <component>
  kubectl get <component> --show-labels
  kubectl get <component> --all-namespaces
  ```

- View detailed information about a component:
  ```bash
  kubectl describe <component> <component_name>
  ```

- Create or update resources from a YAML file:
  ```bash
  kubectl create -f <filename>.yaml   # Create a new resource
  kubectl apply -f <filename>.yaml    # Apply changes to a resource; if already exist then upgrades it
  ```

- Label a resource:
  ```bash
  kubectl label <component> <component_name> key=value
  ```

- Delete a resource:
  ```bash
  kubectl delete <component> <component_name>
  ```

### Nginx Ingress Setup

To use Nginx Ingress in your Minikube cluster, follow these steps:

1. Apply the Nginx Ingress Controller:
   ```bash
   kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.11.2/deploy/static/provider/cloud/deploy.yaml
   ```

2. Run the Minikube tunnel to access the Nginx Ingress controller:
   ```bash
   minikube tunnel
   ```

3. Verify the Ingress is created successfully by running:
   ```bash
   kubectl get ingress
   ```
   - Check the `ADDRESS` column in the output. If it is empty, the ingress has not been created successfully.

Useful resources for Nginx Ingress:

- [Nginx Ingress Documentation](https://kubernetes.github.io/ingress-nginx/deploy/)
- [Nginx Ingress GitHub Repository](https://github.com/kubernetes/ingress-nginx)