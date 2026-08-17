# 🐳 Docker Notes

## What is Docker?

Docker is a platform for developing, shipping, and running applications in **containers**.

- **Without Docker:** "It works on my machine" problem
- **With Docker:** Same environment everywhere (dev, staging, production)

---

## Core Concepts

### Images vs Containers

| | Image | Container |
|---|---|---|
| What | Blueprint/Recipe | Running instance |
| Analogy | Class (OOP) | Object (OOP) |
| State | Static | Dynamic |
| Command | `docker build` | `docker run` |

### Docker Architecture

Dockerfile → docker build → Image → docker run → Container
(recipe) (cooking) (dish) (serving) (eating)


---

## Dockerfile Instructions

```dockerfile
# Base image to build from
FROM python:3.12-rc-bookworm

# Create a volume mount point
VOLUME /app/data

# Set working directory inside container
WORKDIR /app

# Copy files from host to container
COPY . /app

# Run command during image BUILD
RUN pip install --no-cache-dir -r requirements.txt

# Set environment variables
ENV FLASK_APP=app.py

# Add metadata labels to image
LABEL "com.example.vendor"="Big Star Collectibles"
LABEL version="1.0"
LABEL description="The Big Star Collectibles Website."

# Command to run when container STARTS
CMD ["flask", "run", "--host=0.0.0.0"]

# Expose port (documentation only, doesn't publish)
EXPOSE 5000

# Set default executable (can be overridden)
ENTRYPOINT ["python"]
```

### RUN vs CMD vs ENTRYPOINT

| | When | Purpose |
|---|---|---|
| `RUN` | During build | Install packages, setup |
| `CMD` | Container start | Default command (overridable) |
| `ENTRYPOINT` | Container start | Fixed executable (not overridable) |

---

## Docker CLI Commands

### Images

```bash
# List all images
docker images
docker images --all

# Build image from Dockerfile
docker build -t image-name .

# Build with custom Dockerfile name
docker build --file custom.Dockerfile --tag image-name .

# Build without cache (fresh build)
docker build --no-cache -t image-name .

# Build for multiple platforms
docker buildx build -t image-name --load .

# Remove image
docker rmi image-name

# Remove specific version (tag)
docker rmi image-name:tag

# Force remove image
docker rmi -f image-name

# Remove all images at once
docker rmi -f $(docker images -q)

# Pull image from Docker Hub
docker pull image-name:tag

# Get only image IDs
docker images -q
```

### Containers

```bash
# Run container (basic)
docker run image-name

# Run with name
docker run --name my-container image-name

# Run in background (detached)
docker run -d image-name

# Run interactively
docker run -it image-name

# Run and auto-remove when stopped
docker run --rm image-name

# Run with port mapping (host:container)
docker run -p 8080:80 image-name

# Run with environment variable
docker run -e POSTGRES_PASSWORD=password postgres

# Run with volume mount
docker run -v /host/path:/container/path image-name

# Run with bind mount
docker run --mount type=bind,source="${PWD}/folder",target=/app/folder image-name

# Keep container running forever
docker run -d image-name sleep infinity

# List running containers
docker ps

# List all containers (including stopped)
docker ps -a

# Get only container IDs
docker ps -aq

# Stop container
docker stop container-name
docker stop container-id

# Stop all containers
docker stop $(docker ps -q)

# Remove container
docker rm container-name

# Remove all stopped containers
docker rm $(docker ps -aq)

# Force remove running container
docker rm -f container-name
```

### Exec (interact with running container)

```bash
# Run command inside running container
docker exec container-id command
docker exec bc88 date

# Get interactive shell inside container
docker exec --interactive --tty container-id bash
docker exec -it container-id bash

# Short form
docker exec -it bc88 bash
```

### Logs & Inspection

```bash
# View container logs
docker logs container-name
docker logs container-id

# Follow logs in real time
docker logs -f container-name

# Inspect container details
docker inspect container-name

# View container resource usage
docker stats
```

---

## Key Flags Reference

| Flag | Short | Meaning |
|------|-------|---------|
| `--detach` | `-d` | Run in background |
| `--interactive` | `-i` | Keep stdin open |
| `--tty` | `-t` | Allocate terminal |
| `--rm` | | Auto-remove when stopped |
| `--name` | | Name the container |
| `--publish` | `-p` | Port mapping host:container |
| `--env` | `-e` | Set environment variable |
| `--volume` | `-v` | Mount volume |
| `--file` | `-f` | Custom Dockerfile path |
| `--tag` | `-t` | Name/tag the image |
| `--no-cache` | | Build without cache |
| `--load` | | Load buildx image locally |

---

## Volumes & Mounts

### Types:

**1. Volume (Docker managed):**
```bash
docker run -v myvolume:/app/data image-name
```
Docker manages storage location. Best for persistence.

**2. Bind Mount (host folder):**
```bash
docker run -v $PWD/myFolder:/app/folder image-name
# or
docker run --mount type=bind,source="${PWD}/folder",target=/app/folder image-name
```
Links host folder directly. Good for development (live code changes).

### Why Volumes Matter:
- Containers are **ephemeral** (temporary)
- Data dies when container stops
- Volumes = persist data outside container
- Without volume = data lost on container stop

---

## Port Mapping

```bash
docker run -p 8080:80 nginx
```

Your Browser → localhost:8080 → Docker → Container port 80
HOST PORT CONTAINER PORT


- Left side = your machine port
- Right side = container's internal port

---

## Docker Hub

```bash
# Login
docker login

# Push image to Docker Hub
docker tag local-image:tag username/repo:tag
docker push username/repo:tag

# Pull image
docker pull username/repo:tag
```

---

## Image Layers & Caching

- Every Dockerfile instruction = one layer
- Docker caches each layer
- If layer unchanged = uses cache (faster rebuild)
- If layer changed = rebuilds from that point onwards

Layer 1: FROM ubuntu ← cached if unchanged
Layer 2: RUN apt update ← cached if unchanged
Layer 3: COPY . /app ← rebuilt if files changed
Layer 4: RUN pip install ← rebuilt because layer 3 changed


**Best practice:** Put frequently changing instructions (COPY) AFTER rarely changing ones (RUN apt install).

---

## Labels

```dockerfile
# Single label
LABEL version="1.0"

# Multiple labels (efficient - one layer)
LABEL version="1.0" \
      maintainer="soham@example.com" \
      description="My app"

# Separate labels (multiple layers - less efficient)
LABEL version="1.0"
LABEL maintainer="soham@example.com"
```

---

## Common Issues & Fixes

### Password required for postgres:
```bash
docker run -e POSTGRES_PASSWORD=password postgres
```

### Container name already in use:
```bash
docker rm container-name
# then run again
```

### Image not found:
```bash
# Build first
docker build -t image-name .
# then run
docker run image-name
```

### Port already in use:
```bash
# Use different host port
docker run -p 8081:80 nginx
```

### xargs not found (PowerShell):
```powershell
# Use this instead
docker images -q | ForEach-Object { docker rmi $_ }
# or
docker rmi -f $(docker images -q)
```

### WSL Docker not found:
- Open Docker Desktop → Settings → Resources → WSL Integration
- Enable for Ubuntu
- Apply & Restart

---

## Docker vs Virtual Machine

| | Docker Container | Virtual Machine |
|---|---|---|
| Size | MBs | GBs |
| Startup | Seconds | Minutes |
| OS | Shares host OS | Full OS |
| Isolation | Process level | Hardware level |
| Performance | Near native | Overhead |

---

## Dockerfile Best Practices

1. Use specific image tags (`python:3.12` not `python:latest`)
2. Use `.dockerignore` to exclude unnecessary files
3. Combine RUN commands to reduce layers
4. Put COPY after RUN (better caching)
5. Use `--no-cache-dir` with pip
6. Use non-root user (`USER nobody`)
7. Use multi-stage builds for smaller images

---

## Commands Learned in Order

```bash
docker ps                          # list containers
docker run postgres:9.6            # run postgres
docker run -e POSTGRES_PASSWORD=password postgres:9.6
docker images                      # list images
docker build -t our-first-image .  # build image
docker run our-first-image         # run container
docker buildx build -t image --load .
docker run --rm image              # auto remove
docker build --file server.Dockerfile --tag our-first-server .
docker run -d our-first-server     # detached
docker exec bc88 date              # exec command
docker exec -it bc88 bash          # interactive shell
docker ps -aq | xargs docker rm    # remove all containers
docker rmi -f $(docker images -q)  # remove all images
docker run --name=alpine -d alpine sleep infinity
docker run -it eclipse-temurin:21  # java container
docker run -p 8080:80 --rm nginx   # nginx web server
docker run -v "$PWD/website:/usr/share/nginx/html" -p 8080:80 nginx
docker run --mount type=bind,source="${PWD}/test",target=/app/test image
docker build --no-cache -t image:v2 .
```

---

## Resources

- [Docker Official Docs](https://docs.docker.com)
- [Docker Hub](https://hub.docker.com)
- [TechWorld with Nana - Docker Playlist](https://youtube.com/@TechWorldwithNana)
- [LinkedIn Learning - Docker Foundation](https://linkedin.com/learning)
- [LinkedIn Learning - Docker Your First Project](https://github.com/LinkedInLearning/docker-your-first-project-4485003)