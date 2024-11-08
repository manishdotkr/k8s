# Complete Monitoring Stack Setup Guide

## Initial Helm Setup

### Install Helm (Choose one method)

#### Using Curl (Recommended)
```bash
curl https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3 | bash
```

#### Using Package Manager (Ubuntu/Debian)
```bash
curl https://baltocdn.com/helm/signing.asc | gpg --dearmor | sudo tee /usr/share/keyrings/helm.gpg > /dev/null
sudo apt-get install apt-transport-https --yes
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/helm.gpg] https://baltocdn.com/helm/stable/debian/ all main" | sudo tee /etc/apt/sources.list.d/helm-stable-debian.list
sudo apt-get update
sudo apt-get install helm
```

### Add Required Helm Repositories
```bash
# Add Grafana repository
helm repo add grafana https://grafana.github.io/helm-charts

# Add Prometheus repository
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts

# Update repositories
helm repo update
```

## Docker Configuration

### Create Base64 Encoded Docker Config
```bash
# Replace <username>, <password>, and <email> with your actual credentials
echo -n '{"auths":{"ghcr.io":{"username":"<username>","password":"<access-token>","email":"<email>","auth":"'$(echo -n "<username>:<access-token>" | base64)'"}}}' | base64
```

## Component Installation

### Prometheus Setup
```bash
# Install in default namespace
helm install prometheus prometheus-community/prometheus

# Install in monitoring namespace
kubectl create namespace monitoring
helm install --namespace monitoring prometheus prometheus-community/prometheus
```

### Grafana Setup
```bash
# Install in default namespace
helm install grafana grafana/grafana

# Install in monitoring namespace
helm install --namespace monitoring grafana grafana/grafana --set release-namespace=monitoring
```

### Logging Setup (Loki)
```bash
# Basic installation
helm install loki grafana/loki-stack -n logging-ns --set loki.image.tag=2.9.3

# Advanced installation with custom values
helm show values grafana/loki-stack > loki-stack-values.yaml
helm install loki grafana/loki-stack -n <namespace> -f loki-stack-values.yaml

# Upgrade existing installation
helm upgrade loki grafana/loki-stack -n <namespace> -f loki-values.yaml
helm upgrade --install loki grafana/loki-stack --set loki.image.tag=2.9.3 -f loki-stack.yaml
```

## Grafana Configuration

### Dashboard
- Recommended Dashboard: https://grafana.com/grafana/dashboards/13639-logs-app/

### Accessing Grafana Admin Password
```bash
# For default namespace
kubectl get secret grafana -o jsonpath="{.data.admin-password}" | base64 --decode ; echo

# For monitoring namespace
kubectl get secret --namespace monitoring grafana -o jsonpath="{.data.admin-password}" | base64 --decode ; echo
```

## Loki Configuration

### Endpoints and Testing
- Loki Service Endpoint: `http://loki.logging.svc.cluster.local:3100`
- Check readiness: `curl http://loki:3100/ready`
- Check metrics: `curl http://<loki_svc_ip>:3100/metrics`

### API Testing from Grafana Container
```bash
curl http://loki:3100/loki/api/v1/labels
curl http://loki:3100/loki/api/v1/query_range
```

## Additional Resources
- Tutorial Video: https://www.youtube.com/watch?v=UM8NiQLZ4K0
- Troubleshooting Guide: 
  - https://community.grafana.com/t/grafana-unable-to-connect-with-loki-please-check-the-server-logs-for-more-details/119757/5
  - https://github.com/grafana/loki/issues/11557#issuecomment-2014825845