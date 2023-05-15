# docker-kube
## Linux Tweet App Deployment through Docker

This is very simple NGINX website that allows a user to send a tweet. 

It's mostly used as a sample application for Docker 101 workshops. 

To use it:

Build it:
`docker build -t linux-tweet-app:v0.0.1 .`

Run it:
`docker container run -d -p 80:80 --name=linux-tweet-app linux-tweet-app:v0.0.1`

Few Commands:

View:
To view image: `docker images` or `docker image ls`

To view containers (running/stopped): `docker ps -a`

Tag/Pull/Push:
To tag the image: `docker tag linux-tweet-app:v0.01 abhilashindulkar/linux-tweet-app:v0.01`

To pull the image: `docker pull abhilashindulkar/linux-tweet-app:v0.01`

To push the image: `docker push abhilashindulkar/linux-tweet-app:v0.01`

Cleanup:
To delete specific container: `docker rm -f <container-id>`

To remove all running/stopped containers: `docker container prune`

Refer deployed_image.png for successful deployed image.

---

## Linux Tweet App Deployment through Kubernetes

Create a secret to pull/push image into hub.docker.com repository:
`kubectl create secret docker-registry registrycreds --docker-server=https://index.docker.io/v1/ --docker-username=user --docker-password=password --docker-email=abc-xyz@gmail.com`  


Deploy/Service Apply:
To apply all the manifests within namespace develop: `kubectl apply -f k8s/`

CleanUp:
To delete/remove object/app-services: `kubectl delete -f k8s/`


