# Docker Compose Notes

## What is Docker Compose?

Tool for defining and running **multi-container** Docker applications.
Instead of multiple `docker run` commands → one `docker-compose.yml` file.

---

## Why Docker Compose?

**Without Compose (manual):**
```bash
docker network create mongo-network
docker run -d -p 27017:27017 -e MONGO_INITDB_ROOT_USERNAME=admin ...
docker run -d -p 8081:8081 -e ME_CONFIG_MONGODB_SERVER=mongodb ...
```

**With Compose:**
```bash
docker-compose up
```

One command. Everything starts together.

---

## docker-compose.yml Structure

```yaml
version: "3.9"  # obsolete in newer versions, remove it

services:        # define your containers here
  service-name:
    image: image-name
    build: .     # or build from Dockerfile
    ports:
      - "host:container"
    environment:
      KEY: value
    env_file:
      - ./path/to/env_file
    volumes:
      - ./host:/container
    depends_on:
      - other-service
    networks:
      - network-name

volumes:         # named volumes
  volume-name:

networks:        # custom networks
  network-name:
```

---

## Real Example (MongoDB + Mongo Express + Node App)

```yaml
services:
  mongodb:
    image: mongo
    ports:
      - "27017:27017"
    environment:
      MONGO_INITDB_ROOT_USERNAME: admin
      MONGO_INITDB_ROOT_PASSWORD: password
    volumes:
      - mongo-data:/data/db

  mongo-express:
    image: mongo-express
    ports:
      - "8081:8081"
    environment:
      ME_CONFIG_MONGODB_URL: mongodb://admin:password@mongodb:27017/
      ME_CONFIG_BASICAUTH: false
    depends_on:
      - mongodb

  app:
    build: .
    ports:
      - "3000:3000"
    depends_on:
      - mongodb

volumes:
  mongo-data:
```

---

## Key Concepts

### Services
Each service = one container.
Service name = hostname on the network.

```yaml
services:
  mongodb:     # other containers reach this via "mongodb:27017"
  app:         # other containers reach this via "app:3000"
```

### depends_on
Controls startup order.
```yaml
mongo-express:
  depends_on:
    - mongodb   # mongodb starts before mongo-express
```
**Note:** Only waits for container to START, not for app inside to be ready.

### Networks
By default Compose creates one network for all services.
All services can talk to each other by service name.

Custom network:
```yaml
services:
  app:
    networks:
      - my-network

networks:
  my-network:
```

### Volumes

**Bind mount (host folder):**
```yaml
volumes:
  - ./mysql:/docker-entrypoint-initdb.d:ro
```
`ro` = read only

**Named volume (Docker managed):**
```yaml
volumes:
  - mongo-data:/data/db

volumes:
  mongo-data:   # declare at bottom
```
Named volumes persist data between container restarts.

### Environment Variables

**Inline:**
```yaml
environment:
  MONGO_INITDB_ROOT_USERNAME: admin
  MONGO_INITDB_ROOT_PASSWORD: password
```

**From file:**
```yaml
env_file:
  - ./mysql/env_vars
```

env_vars file content:

MYSQL_ROOT_PASSWORD=password
MYSQL_DATABASE=mydb
MYSQL_USER=user
MYSQL_PASSWORD=password


### Build vs Image

**Use existing image:**
```yaml
services:
  db:
    image: mongo
```

**Build from Dockerfile:**
```yaml
services:
  app:
    build: .          # Dockerfile in current dir
    # or
    build:
      context: .
      dockerfile: custom.Dockerfile
```

---

## Docker Compose Commands

```bash
# Start all services (foreground)
docker-compose up

# Start all services (background/detached)
docker-compose up -d

# Start specific service only
docker-compose up servicename

# Stop and remove containers + networks
docker-compose down

# Stop and remove + delete volumes
docker-compose down -v

# Stop without removing
docker-compose stop

# Rebuild images before starting
docker-compose up --build

# View running services
docker-compose ps

# View logs
docker-compose logs

# Follow logs in real time
docker-compose logs -f

# Follow specific service logs
docker-compose logs -f servicename

# Execute command in running service
docker-compose exec servicename bash

# Run one-off command in new container
docker-compose run servicename command

# List images used
docker-compose images

# Pull latest images
docker-compose pull
```

---

## Common Issues & Fixes

### version attribute warning:

the attribute version is obsolete

Remove `version: "3.9"` from yaml file.

### env file not found:

env file ./mysql/env_vars not found

Create the file at exact path specified.

### Container name conflict:

container name already in use

```bash
docker-compose down
docker-compose up -d
```

### Service can't connect to another:

mongo: Name does not resolve

Check service names match exactly in env variables.
Service name = hostname. Case sensitive.

### ME_CONFIG_MONGODB_SERVER ignored:
Use full URL instead:
```yaml
ME_CONFIG_MONGODB_URL: mongodb://admin:password@mongodb:27017/
```

---

## Compose vs Manual Docker Run

| | Manual `docker run` | Docker Compose |
|---|---|---|
| Start | Multiple commands | `docker-compose up` |
| Stop | Multiple `docker stop` | `docker-compose down` |
| Network | Create manually | Auto-created |
| Config | Flags in terminal | YAML file |
| Reproducible | Hard | Easy |
| Team sharing | Hard | Commit yaml to git |

---

## Real World Use Cases

1. **Local development** — app + database + cache together
2. **Testing** — spin up full stack for integration tests
3. **CI/CD** — run tests in isolated environment
4. **Microservices** — multiple services working together

---

## What Compose Does Automatically

- Creates a **network** for all services
- Assigns **DNS** (service name = hostname)
- Manages **startup order** (depends_on)
- Handles **volume** creation
- Names containers as `projectname_servicename_1`

---

## Lessons Learned (Real Bugs Fixed)

1. `ME_CONFIG_MONGODB_SERVER=mongo` failed because container named `mongodb` not `mongo` — names must match exactly
2. Old mongo-express image ignored `ME_CONFIG_MONGODB_SERVER` — use `ME_CONFIG_MONGODB_URL` instead
3. Spaces in folder paths break docker volume mounts — use quotes
4. `env_file` path must be exact relative to docker-compose.yml location
5. `depends_on` only waits for container start, not app readiness

---

## Resources

- [Docker Compose Docs](https://docs.docker.com/compose/)
- [Compose File Reference](https://docs.docker.com/compose/compose-file/)