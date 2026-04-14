## Linux Tweet App Deployment through Kubernetes

1. [Prebuilt image deployment](#1-prebuilt-image-deployment)
2. [Kaniko build & deploy](#2-kaniko-build--deploy)
3. [Deploy with Ingress](#3-deploy-with-ingress)

---

### 1. Prebuilt image deployment

Uses a pre-pushed Docker Hub image directly in the deployment manifest.

**Create registry secret:**

```bash
kubectl create secret docker-registry registrycreds \
  --docker-server=https://index.docker.io/v1/ \
  --docker-username=<username> \
  --docker-password=<password>
```

**Deploy:**

```bash
kubectl apply -f prebuilt-image/
```

**Cleanup:**

```bash
kubectl delete -f prebuilt-image/
```

---

### 2. Kaniko build & deploy

Builds the Docker image inside the cluster using [Kaniko](https://github.com/GoogleContainerTools/kaniko) (no Docker daemon required), pushes it to Docker Hub, then deploys.

**How it works:**

1. A Kaniko `Job` clones the repo via `--context=git://`, builds from `docker/Dockerfile`, and pushes to `abhilashindulkar/linux-tweet-app:v0.01`
2. A `Deployment` pulls that image and serves the app
3. A `Service` (LoadBalancer) exposes port 80

**Step 1 -- Create registry credentials:**

Kaniko needs push access. Create a `docker-config` secret from your Docker config:

```bash
# Option A: From existing docker login
kubectl create secret generic docker-config \
  --from-file=.dockerconfigjson=$HOME/.docker/config.json \
  --type=kubernetes.io/dockerconfigjson \
  -n develop

# Option B: Create directly
kubectl create secret docker-registry docker-config \
  --docker-server=https://index.docker.io/v1/ \
  --docker-username=<username> \
  --docker-password=<password> \
  -n develop
```

**Step 2 -- Create namespace:**

```bash
kubectl apply -f build-deploy/namespace.yml
```

**Step 3 -- Run Kaniko build:**

```bash
kubectl apply -f build-deploy/kaniko-build-job.yml
```

Monitor the build:

```bash
kubectl logs -f job/kaniko-build -n develop
```

Wait for completion:

```bash
kubectl wait --for=condition=complete job/kaniko-build -n develop --timeout=300s
```

**Step 4 -- Deploy the app:**

```bash
kubectl apply -f build-deploy/deployment.yml
kubectl apply -f build-deploy/service.yml
```

**Rebuild with a new version:**

To build a new image version, delete the old job and create a new one. Update the `--destination` tag in `kaniko-build-job.yml` and the `image` tag in `deployment.yml` accordingly.

```bash
kubectl delete job kaniko-build -n develop
# edit kaniko-build-job.yml with new tag
kubectl apply -f build-deploy/kaniko-build-job.yml
```

**Cleanup:**

```bash
kubectl delete -f build-deploy/
```

---

### 3. Deploy with Ingress

Two microservices (linux-tweet-app & tomcat) behind an NGINX Ingress controller with path-based routing.

**Deploy microservices:**

```bash
kubectl apply -f deploy-with-ingress/tweet/
kubectl apply -f deploy-with-ingress/tomcat/
```

**Install NGINX Ingress Controller:**

```bash
helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
helm repo update
helm install nginx-ingress ingress-nginx/ingress-nginx
```

Verify:

```bash
kubectl get deployment nginx-ingress-ingress-nginx-controller
kubectl get service nginx-ingress-ingress-nginx-controller
```

Refer to https://github.com/kubernetes/ingress-nginx/ for version-specific installation.

**Apply Ingress resource:**

```bash
kubectl apply -f deploy-with-ingress/ingress.yml
```

**Access:**

```bash
curl http://app.local.io/tweet
curl http://app.local.io/tomcat
curl http://app.local.io/tomcat/SampleWebApp
```

**Cleanup:**

```bash
kubectl delete -f deploy-with-ingress/ingress.yml
helm uninstall nginx-ingress
kubectl delete -f deploy-with-ingress/tweet/
kubectl delete -f deploy-with-ingress/tomcat/
```
