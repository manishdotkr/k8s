# k8 minikube

### access minikube
```
minikube start        # starts the minikube
minikube status         # gives minikube status
minikube dashboard    # creates and shows minikube dashboard
```

### kubectl common commands

- List resources (e.g., `pods`, `deployments`, `svc`, `ingress`, `namespaces`):
```
kubectl get <component>                     
kubectl get <component> --show-labels       
kubectl get <component> --all-namespaces   
kubectl describe <component>               
kubectl create -f <filename>.yaml          
kubectl apply -f <filename>.yaml            
kubectl delete <component> <component_name> 
kubectl label <component> <component_name> key=value 
```