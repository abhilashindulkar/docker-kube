### Kustomize

Commands

1. kustomize build - lists all the k8s manifests and kustomization file configs, combines/transforms the manifests. It gives stdout result; doesn't apply/update/delete the configs.

`kustomize build k8s/` 

2. Apply configs to k8s environment -

`kustomize build k8s/ | kubectl apply -f -`

or

`kubectl apply -k k8s/`

3. Delete the resources -

`kustomize build k8s/ | kubectl delete -f -`

or

`kubectl delete -k k8s/`
