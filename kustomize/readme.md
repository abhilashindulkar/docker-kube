### Kustomize

Build and apply overlays per environment. Do not apply all environments at once.

**Preview manifests** (dry-run, stdout only):

```bash
kustomize build kustomize/dev/
kustomize build kustomize/uat/
kustomize build kustomize/prd/
```

**Apply to cluster:**

```bash
kustomize build kustomize/dev/ | kubectl apply -f -
# or
kubectl apply -k kustomize/dev/
```

**Delete resources:**

```bash
kustomize build kustomize/dev/ | kubectl delete -f -
# or
kubectl delete -k kustomize/dev/
```
