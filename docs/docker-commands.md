# LocalGPT – Docker Commands Reference

A collection of useful Docker and Docker Compose commands used in the LocalGPT project.

## 1. Docker Version and Information

```powershell
docker --version
docker compose version
docker info
```

## 2. Docker Images

```powershell
# Pull an image
docker pull ollama/ollama:latest

# List downloaded images
docker images

# Remove an image
docker rmi IMAGE_NAME
```

## 3. Docker Containers

```powershell
# List running containers
docker ps

# List all containers
docker ps -a

# View container logs
docker logs localgpt-ollama

# Follow container logs
docker logs -f localgpt-ollama

# Execute a command inside a container
docker exec -it localgpt-ollama bash

# Inspect container details
docker inspect localgpt-ollama

# Monitor container resource usage
docker stats
```

## 4. Docker Compose

```powershell
# Start all services
docker compose up -d

# Stop all services
docker compose stop

# Stop and remove containers
docker compose down

# Build and start services
docker compose up -d --build

# Pull updated images
docker compose pull

# View running services
docker compose ps

# View logs
docker compose logs

# Follow logs
docker compose logs -f

# Restart services
docker compose restart

# Restart a particular service
docker compose restart ollama
```

## 5. Docker Networks

```powershell
# List networks
docker network ls

# Inspect the LocalGPT network
docker network inspect localgpt-network

# Remove a network
docker network rm localgpt-network
```

## 6. Docker Volumes

```powershell
# List volumes
docker volume ls

# Inspect Ollama volume
docker volume inspect localgpt_ollama-data

# Inspect Open WebUI volume
docker volume inspect localgpt_openwebui-data

# Display Docker storage usage
docker system df -v
```

## 7. Ollama Commands

```powershell
# Download an AI model
docker compose exec ollama ollama pull llama3.2:1b

# List downloaded models
docker compose exec ollama ollama list

# Run an AI model
docker compose exec ollama ollama run llama3.2:1b

# Check Ollama API
Invoke-RestMethod http://localhost:11434/api/tags
```

## 8. Cleanup Commands

```powershell
# Remove stopped containers
docker container prune

# Remove unused images
docker image prune

# Remove unused networks
docker network prune

# Remove unused volumes
docker volume prune

# Remove unused Docker resources
docker system prune
```

**Warning:** Avoid `docker compose down -v` and `docker volume prune` when you want to preserve LocalGPT's AI models and chat history.

## 9. LocalGPT Application

```powershell
# Start LocalGPT
docker compose up -d

# Check application containers
docker compose ps

# Access Open WebUI
# http://localhost:3000

# Access Ollama API
# http://localhost:11434/api/tags

# Stop LocalGPT
docker compose down
```