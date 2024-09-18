## Extra Info

1. **Port Forwarding Option (Alternative to `minikube tunnel`)**:
   If users don’t want to or cannot use `minikube tunnel`, you can mention port forwarding as an alternative:
   ```bash
   kubectl port-forward <pod_name> <local_port>:<container_port>
   ```
   This might help for debugging or simpler cases where tunneling is unnecessary.

2. **Namespace Context**:
   If users are working with multiple namespaces, a reminder to set the correct namespace might be helpful:
   ```bash
   kubectl config set-context --current --namespace=<namespace>
   ```

3. **Expose Service Command** (for testing without ingress):
   To give users an option to expose services quickly, without setting up ingress, you can mention the following command:
   ```bash
   kubectl expose deployment <deployment_name> --type=NodePort --port=<port>
   ```

4. **Logs and Debugging Section**:
   Adding a short section on how to check logs and troubleshoot issues could be useful. For instance:
   ```bash
   kubectl logs <pod_name>                # Check logs of a pod
   kubectl get events                     # Get events for debugging
   kubectl describe ingress <ingress_name> # Troubleshoot ingress issues
   ```

5. **Ingress Host Configuration**:
   Users might need guidance on how to configure the `hosts` file to map domain names to the Minikube IP for accessing the Ingress:
   ```bash
   sudo nano /etc/hosts
   # Add:
   <minikube_ip> <ingress_domain>
   ```