## Skaffold - Linux Tweet App

[Skaffold](https://skaffold.dev/) handles the build-push-deploy workflow in a single command with hot-reload for local development.

### Prerequisites

- [Skaffold CLI](https://skaffold.dev/docs/install/)
- A running Kubernetes cluster (minikube, kind, GKE, etc.)
- Docker (for local builds) or registry credentials (for in-cluster Kaniko builds)

### Profiles

| Profile | Build | Deploy | Use case |
|---------|-------|--------|----------|
| `dev` (default) | Local Docker | kubectl manifests | Local development |
| `helm` | Local Docker | Helm chart | Helm-based deployment |
| `kaniko` | In-cluster Kaniko | kubectl manifests | No local Docker daemon |

### Usage

All commands should be run from the `skaffold/` directory.

**Dev mode (build + deploy + watch for changes):**

```bash
cd skaffold
skaffold dev -p dev
```

Skaffold watches for file changes, rebuilds the image, and redeploys automatically. Press `Ctrl+C` to tear down.

**One-time deploy:**

```bash
skaffold run -p dev
```

**Deploy with Helm:**

```bash
skaffold run -p helm
```

**Build with Kaniko (in-cluster, no Docker needed):**

Requires a `docker-config` secret in the `develop` namespace for registry push access.

```bash
kubectl create secret docker-registry docker-config \
  --docker-server=https://index.docker.io/v1/ \
  --docker-username=<username> \
  --docker-password=<password> \
  -n develop

skaffold run -p kaniko
```

**Cleanup:**

```bash
skaffold delete -p dev
```

### How it works

1. **Build** -- Skaffold builds the image using `docker/Dockerfile` with the repo root as context
2. **Tag** -- Skaffold auto-generates a unique tag (git commit SHA by default)
3. **Push** -- Pushes to Docker Hub (or uses local images with minikube)
4. **Deploy** -- Applies the K8s manifests and injects the built image tag automatically
5. **Watch** (dev mode) -- Monitors source files and repeats the cycle on changes
