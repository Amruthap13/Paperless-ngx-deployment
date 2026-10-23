
# 04 - Paperless-ngx Configuration

## Overview

Paperless-ngx was configured using a Docker Compose YAML file located at:

```text
/opt/paperless/docker-compose.yml
```

Sensitive values are stored separately in:

```text
/opt/paperless/.env
```

## Services

### 1. Paperless-ngx

- Service name: `webserver`
- Image: `ghcr.io/paperless-ngx/paperless-ngx:latest`
- Container port: 8000
- Host port: 8000

Paperless-ngx provides the document management interface, document processing, and search functionality.

### 2. PostgreSQL

- Service name: `db`
- Image: `postgres:16-alpine`
- Database name: `paperless`
- Database user: `paperless`

PostgreSQL stores structured application information, including document metadata and other records.

The database password is supplied through the environment file.

### 3. Redis

- Service name: `broker`
- Image: `redis:7-alpine`

Redis supports background task queuing and coordination for document processing.

## Environment Variables

The Paperless service uses the following configuration:

| Variable | Purpose |
|---|---|
| `PAPERLESS_REDIS` | Redis connection address |
| `PAPERLESS_DBENGINE` | Database engine |
| `PAPERLESS_DBHOST` | PostgreSQL service hostname |
| `PAPERLESS_DBNAME` | Database name |
| `PAPERLESS_DBUSER` | Database username |
| `PAPERLESS_DBPASS` | Database password from `.env` |
| `PAPERLESS_SECRET_KEY` | Application secret key |
| `PAPERLESS_TIME_ZONE` | Application time zone |
| `PAPERLESS_OCR_LANGUAGE` | Default OCR language |

The configured values include:

- Database engine: PostgreSQL
- Database host: `db`
- Redis host: `broker`
- Time zone: `Asia/Kolkata`
- OCR language: `eng`

Passwords and secret keys are not included in this documentation.

## Port Mapping

The Compose file contains:

```yaml
ports:
  - "8000:8000"
```

The first port is the host port, and the second is the container port.

The application was accessed through port 8000 on the Azure VM.

## Persistent Storage

The deployment uses the following Docker volumes:

| Volume | Container destination |
|---|---|
| `pgdata` | `/var/lib/postgresql/data` |
| `redisdata` | `/data` |
| `data` | `/usr/src/paperless/data` |
| `media` | `/usr/src/paperless/media` |

The document directories are mounted using bind mounts:

| Host directory | Container destination |
|---|---|
| `./consume` | `/usr/src/paperless/consume` |
| `./export` | `/usr/src/paperless/export` |

Named volumes and bind mounts keep data outside the container's writable layer.

## Docker Networking

Docker Compose creates a project network for the services.

Paperless connects to PostgreSQL using the service name `db` and to Redis using `broker`.

These service names are resolved through Docker's internal DNS.

## Restart Policy

The services use:

```yaml
restart: unless-stopped
```

This configures Docker to restart the containers after many unexpected exits and when Docker restarts, unless the containers have been explicitly stopped.

## Result

The application was configured with PostgreSQL, Redis, port mapping, environment variables, and persistent storage using Docker Compose.
