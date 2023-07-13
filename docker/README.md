## Linux Tweet App Deployment through Docker

It's mostly used as a sample application for Docker deployment.

1. Manual
2. docker-compose

*Manual*

* Build:
`docker build -f docker/Dockerfile -t linux-tweet-app:v0.0.1 .`

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

---

*docker-compose*

* Deploy:
`docker-compose up -d`

* Check logs:
`docker-compose logs linux-tweet-app`

* Exec into container:
`docker-compose exec linux-tweet-app bash`

* Stop/Start container:
`docker-compose stop/start linux-tweet-app`

* Kill/Remove container:
`docker-compose kill/rm linux-tweet-app`

__NOTE__ - Refer deployed_image.png for successful deployed image.

