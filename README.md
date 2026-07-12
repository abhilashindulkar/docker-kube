# docker-kube
## Linux Tweet App Deployment

A static NGINX website that displays a Twitter share link. Used as a sample application to demonstrate multiple container and Kubernetes deployment patterns.

### Application

- **Source:** `src/index.html` — single-page static site served by NGINX
- **Image:** `abhilashindulkar/linux-tweet-app:v0.0.1`
- **Base image:** `nginx:1.27-alpine`

### Deployment methods

- [x] Docker
  - [x] By executing docker commands manually
  - [x] Through docker-compose
- [x] Kubernetes
  - [x] Prebuilt image from Docker Hub
  - [x] In-cluster build with Kaniko (no Docker daemon required)
  - [x] Multi-service deployment with NGINX Ingress
- [x] Helm Chart
- [x] Kustomize (dev / uat / prd overlays)
- [x] Skaffold

### Repository structure

```
docker/       # Dockerfile and docker-compose
src/          # Application source (index.html)
k8s/          # Raw Kubernetes manifests (3 patterns)
helm/         # Helm chart for the app
kustomize/    # Kustomize base + dev/uat/prd overlays
skaffold/     # Skaffold config + manifests
```

See the README in each directory for usage instructions.
