# LocalGPT – System Architecture

## Overview

LocalGPT is a locally hosted AI assistant built entirely using Docker. It uses Ollama to run large language models locally and Open WebUI to provide a browser-based chat interface.

Docker Compose manages the application services, networking, and persistent storage.

## Architecture

```text
                 User Browser
                localhost:3000
                       |
                       v
              Open WebUI Container
                 Port: 8080
                       |
                       v
               Docker Network
                localgpt-network
                       |
                       v
                Ollama Container
                 Port: 11434
                       |
                       v
                 Llama 3.2 1B
                  AI Model
```

## Components

### 1. Ollama
- Runs and manages local AI models.
- Provides an HTTP API on port 11434.
- Downloads and stores model files.
- Docker Image: `ollama/ollama:latest`

### 2. Open WebUI
- Provides the web-based chat interface.
- Connects to Ollama through the Docker network.
- Stores chat history and application data.
- Docker Image: `ghcr.io/open-webui/open-webui:main`

### 3. Docker Compose
- Manages both application containers.
- Configures port mappings.
- Creates the Docker bridge network.
- Manages persistent volumes.

## Port Mapping

| Service | Host Port | Container Port |
|---|---:|---:|
| Open WebUI | 3000 | 8080 |
| Ollama | 11434 | 11434 |

Access the application at `http://localhost:3000`.

## Persistent Storage

Two named Docker volumes are used.

| Volume | Container Mount Path | Purpose |
|---|---|---|
| `ollama-data` | `/root/.ollama` | Stores AI models |
| `openwebui-data` | `/app/backend/data` | Stores chat and application data |

These volumes preserve data even when containers are removed and recreated.

## Container Networking

Both containers communicate through a custom Docker bridge network called `localgpt-network`.

Open WebUI connects to Ollama using:

`http://ollama:11434`

Docker's internal DNS resolves the service name `ollama` to the corresponding container.

## Technology Stack

- Docker
- Docker Compose
- Ollama
- Open WebUI
- Llama 3.2 1B
- Docker Volumes
- Docker Bridge Networking