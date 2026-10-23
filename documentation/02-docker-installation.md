
# 02 - Docker Installation

## Objective

Install Docker Engine and Docker Compose on the Ubuntu virtual machine to run Paperless-ngx and its supporting services in containers.

## Steps Performed

### 1. Update Ubuntu

```bash
sudo apt update
sudo apt upgrade -y
```

### 2. Install Required Packages

```bash
sudo apt install -y ca-certificates curl
```

### 3. Add Docker's Official Repository

Create the directory for repository keys:

```bash
sudo install -m 0755 -d /etc/apt/keyrings
```

Download the Docker signing key:

```bash
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg \
  -o /etc/apt/keyrings/docker.asc
```

Set its permissions:

```bash
sudo chmod a+r /etc/apt/keyrings/docker.asc
```

Configure the repository:

```bash
sudo tee /etc/apt/sources.list.d/docker.sources > /dev/null <<EOF
Types: deb
URIs: https://download.docker.com/linux/ubuntu
Suites: $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}")
Components: stable
Architectures: $(dpkg --print-architecture)
Signed-By: /etc/apt/keyrings/docker.asc
EOF
```

Refresh the package list:

```bash
sudo apt update
```

### 4. Install Docker

```bash
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

### 5. Start Docker

```bash
sudo systemctl enable --now docker
```

### 6. Verify the Installation

Check Docker:

```bash
docker --version
```

Check Docker Compose:

```bash
docker compose version
```

Check the service status:

```bash
sudo systemctl status docker --no-pager
```

Test Docker by running a sample container:

```bash
sudo docker run hello-world
```

## Components Installed

- Docker Engine: Runs containers.
- Docker CLI: Provides commands to manage Docker.
- containerd: Manages container lifecycle operations underneath Docker.
- Docker Compose plugin: Manages multi-container applications using YAML configuration.
- Docker Buildx: Provides container image-building functionality.

## Result

Docker Engine and the Docker Compose plugin were installed and verified successfully on the Azure virtual machine.
