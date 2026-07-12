## Linux Tweet App — Helm Deployment

The chart lives at `helm/linux-tweet-app/`. It deploys the app as a Kubernetes `Deployment` + `Service`, with optional `Ingress` and `HorizontalPodAutoscaler` support.

### Prerequisites

- [Helm 3](https://helm.sh/docs/intro/install/)
- A running Kubernetes cluster

### Install

```bash
helm install linux-tweet-app helm/linux-tweet-app/
```

Install into a specific namespace:

```bash
helm install linux-tweet-app helm/linux-tweet-app/ -n develop --create-namespace
```

### Upgrade

```bash
helm upgrade linux-tweet-app helm/linux-tweet-app/
```

### Uninstall

```bash
helm uninstall linux-tweet-app
```

### Lint and dry-run

```bash
helm lint helm/linux-tweet-app/
helm install linux-tweet-app helm/linux-tweet-app/ --dry-run --debug
```

### Common value overrides

| Flag | Default | Description |
|------|---------|-------------|
| `image.tag` | `v0.0.1` | Image tag to deploy |
| `replicaCount` | `1` | Number of replicas |
| `service.type` | `LoadBalancer` | Service type (`ClusterIP`, `NodePort`, `LoadBalancer`) |
| `ingress.enabled` | `false` | Enable Ingress resource |
| `autoscaling.enabled` | `false` | Enable HorizontalPodAutoscaler |

**Example — enable ingress:**

```bash
helm install linux-tweet-app helm/linux-tweet-app/ \
  --set ingress.enabled=true \
  --set ingress.className=nginx \
  --set "ingress.hosts[0].host=tweet.local" \
  --set "ingress.hosts[0].paths[0].path=/" \
  --set "ingress.hosts[0].paths[0].pathType=Prefix"
```

**Example — enable autoscaling:**

```bash
helm install linux-tweet-app helm/linux-tweet-app/ \
  --set autoscaling.enabled=true \
  --set autoscaling.minReplicas=2 \
  --set autoscaling.maxReplicas=5
```

### Package and host the chart

```bash
helm package helm/linux-tweet-app/
helm repo index . --url https://<your-repo-url>
```

### Useful links

- [Helm docs](https://helm.sh/docs/)
- [Artifact Hub](https://artifacthub.io/)
- [Bitnami charts](https://github.com/bitnami/charts/tree/main/bitnami)
