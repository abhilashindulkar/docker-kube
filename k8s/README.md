## Linux Tweet App Deployment through Kubernetes

*   Create a secret to pull/push image into hub.docker.com repository:
`kubectl create secret docker-registry registrycreds --docker-server=https://index.docker.io/v1/ --docker-username=user --docker-password=password --docker-email=abc-xyz@gmail.com`  


* Deploy/Service Apply:
To apply all the manifests within namespace develop: `kubectl apply -f k8s/`

* CleanUp:
To delete/remove object/app-services: `kubectl delete -f k8s/`
