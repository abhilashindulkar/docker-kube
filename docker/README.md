## Linux Tweet App Deployment through Docker

This is very simple NGINX website that allows a user to send a tweet. 

It's mostly used as a sample application for Docker deployment. 

To use it:

* Build:
`docker build -t linux-tweet-app:v0.0.1 .`

* Run:
`docker container run -d -p 80:80 --name=linux-tweet-app linux-tweet-app:v0.0.1`

*Few Commands*:

* View:
To view image: `docker images` or `docker image ls`

To view containers (running/stopped): `docker ps -a`

* Tag/Pull/Push:
To tag the image: `docker tag linux-tweet-app:v0.01 abhilashindulkar/linux-tweet-app:v0.01`

To pull the image: `docker pull abhilashindulkar/linux-tweet-app:v0.01`

To push the image: `docker push abhilashindulkar/linux-tweet-app:v0.01`

* Cleanup:
To delete specific container: `docker rm -f <container-id>`

To remove all running/stopped containers: `docker container prune`

__NOTE__ - Refer deployed_image.png for successful deployed image.
