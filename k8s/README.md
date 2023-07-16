## Linux Tweet App Deployment through Kubernetes

1. Applying manifests with prebuilt docker images.
2. Deploy applications with ingress, ingress controller.
3. Build docker images through Kaniko executor, deploy objects into kubernetes cluster.

---

1. Applying manifests with prebuilt docker images.
*   Create a secret to pull/push image into hub.docker.com repository:
`kubectl create secret docker-registry registrycreds --docker-server=https://index.docker.io/v1/ --docker-username=user --docker-password=password --docker-email=abc-xyz@gmail.com`  


* Deploy/Service Apply:
To apply all the manifests within namespace develop: `kubectl apply -f prebuilt-image/`

* CleanUp:
To delete/remove object/app-services: `kubectl delete -f prebuilt-image/`

2. Deploy applications with ingress, ingress controller.
* Use the manifests within deploy-with-ingress folder.
It has two microservices, namely a linux-tweet-app & tomcat webapp.

* Tweet Microservice Deploy/Service Apply:
To apply all the manifests within namespace default: `kubectl apply -f deploy-with-ingress/tweet/`

* Tomcat Microservice Deploy/Service Apply:
To apply all the manifests within namespace default: `kubectl apply -f deploy-with-ingress/tomcat/`

Note - Services can either be exposed through NodePort or default type ClusterIP.

Once the manifests are applied, Follow the below instruction to create NGINX ingress controller.

* Create NGINX Ingress Controller.

  - Before you deploy the NGINX Ingress Helm chart to the GKE cluster, add the nginx-stable Helm repository in Cloud Shell:
```
helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
helm repo update
```

  - Deploy an NGINX controller Deployment and Service by running the following command:


`helm install nginx-ingress ingress-nginx/ingress-nginx`
  - Verify that the nginx-ingress-controller Deployment and Service are deployed to the GKE cluster:

```
kubectl get deployment nginx-ingress-ingress-nginx-controller
kubectl get service nginx-ingress-ingress-nginx-controller
```

Note - Refer https://github.com/kubernetes/ingress-nginx/ for specific versioned NGINX ingress controller deployment.

* Apply ingress.yaml manifest that holds complex path based routing instructions to deployed microservices.

`kubectl apply -f deploy-with-ingress/ingress.yaml`

  - Access application through defined host along with right context paths.
```
curl -v https://app.local.io/tweet
curl -v https://app.local.io/tomcat
curl -v https://app.local.io/tomcat/SampleWebApp
```

* Cleanup.
  - Delete the Ingress Resource object: `kubectl delete -f deploy-with-ingress/ingress.yaml`
  - Delete the NGINX Ingress Helm chart: `helm del nginx-ingress`
  - Delete Microservices from Cluster: 
```
kubectl delete -f deploy-with-ingress/tweet/
kubectl delete -f deploy-with-ingress/tomcat/
```