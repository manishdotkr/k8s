## Changelog

### Version 2.0 - Nginx Basic Deployment

**Branch**: `main`

#### Features:
- **MONITORING.md**:
  - Setup Helm
  - Install Loki Helm Charts
  - Install grafana Helm Charts
- **Readme.md**:
  - Added all k8s commands

---

### Version 1.0 - Nginx Basic Deployment

**Branch**: `release/v1.0`

#### Features:
- **Nginx Deployment**:
  - nginx-deployment.yaml: setting up the pods and its replica count
  - nginx-service.yaml: setting up the svc to access the pods
  - nginx-ingress.yaml: setting up the ingress to allow traffic from outside k8s

---

### Version 0.0 - Initial Release

**Branch**: `main`

#### Features:
- **Initial Commit**:
  - pod.yaml: for creating basic pod
  - deployment.yaml: for creating basic deployment
  