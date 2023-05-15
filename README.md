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

Cleanup:
To delete specific container: `docker rm -f <container-id>`

To remove all running/stopped containers: `docker container prune`

Refer deployed_image.png for successful deployed image.

---

