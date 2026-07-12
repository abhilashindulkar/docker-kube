## Linux Tweet App — Docker Deployment

Two ways to run the app locally: manually with Docker CLI or with docker-compose.

> All commands should be run from the **repository root**, not from the `docker/` directory (the build context is the repo root).

---

### Manual

**Build:**

```bash
docker build -f docker/Dockerfile -t linux-tweet-app:v0.0.1 .
```

**Run:**

```bash
docker container run -d -p 80:80 --name=linux-tweet-app linux-tweet-app:v0.0.1
```

**Useful commands:**

```bash
# List images
docker images

# List containers (running and stopped)
docker ps -a

# Tag for Docker Hub
docker tag linux-tweet-app:v0.0.1 abhilashindulkar/linux-tweet-app:v0.0.1

# Push to Docker Hub
docker push abhilashindulkar/linux-tweet-app:v0.0.1

# Pull from Docker Hub
docker pull abhilashindulkar/linux-tweet-app:v0.0.1

# Remove a specific container
docker rm -f <container-id>

# Remove all stopped containers
docker container prune
```

---

### docker-compose

**Deploy:**

```bash
docker-compose -f docker/docker-compose.yaml up -d
```

**Check logs:**

```bash
docker-compose -f docker/docker-compose.yaml logs linux-tweet-app
```

**Exec into container:**

```bash
docker-compose -f docker/docker-compose.yaml exec linux-tweet-app sh
```

**Stop / Start:**

```bash
docker-compose -f docker/docker-compose.yaml stop linux-tweet-app
docker-compose -f docker/docker-compose.yaml start linux-tweet-app
```

**Tear down:**

```bash
docker-compose -f docker/docker-compose.yaml down
```
