## Linux Tweet App — Kustomize Deployment

Three overlays on top of a shared base: `dev`, `uat`, and `prd`. Each overlay gets its own namespace, name suffix, and environment label. UAT scales to 2 replicas; prd pins to image tag `v0.0.2`.

### Structure

```
kustomize/
├── base/          # Shared Deployment, Service, Namespace (namespace: base)
├── dev/           # namespace: dev,  suffix: -dev,  replicas: 1
├── uat/           # namespace: uat,  suffix: -uat,  replicas: 2 (patch)
└── prd/           # namespace: prd,  suffix: -prd,  image tag: v0.0.2
```

### Preview manifests (dry-run, no cluster changes)

```bash
kustomize build kustomize/dev/
kustomize build kustomize/uat/
kustomize build kustomize/prd/
```

### Apply to cluster

```bash
# Using kustomize CLI
kustomize build kustomize/dev/ | kubectl apply -f -

# Using kubectl built-in kustomize support
kubectl apply -k kustomize/dev/
kubectl apply -k kustomize/uat/
kubectl apply -k kustomize/prd/
```

### Delete resources

```bash
kustomize build kustomize/dev/ | kubectl delete -f -
# or
kubectl delete -k kustomize/dev/
```

> Apply one overlay at a time. Do not apply multiple overlays simultaneously since they share the same base resources.
