
# Paperless-ngx Deployment on Azure VM

## Project Overview

This project demonstrates the deployment of Paperless-ngx, a self-hosted document management system, on an Azure Virtual Machine running Ubuntu Server.

The application is deployed using Docker Compose, with PostgreSQL for database storage and Redis for background task processing.

The deployment was tested by accessing the Paperless web interface, uploading a sample PDF, and searching for text within the document.

## Architecture

```text
User / Web Browser
        |
        | HTTP - Port 8000
        v
Azure Virtual Machine
Ubuntu Server 24.04 LTS
        |
        v
Docker Compose
        |
        +----------------------+
        |          |           |
        v          v           v
    Paperless   PostgreSQL    Redis
      -ngx       Database     Broker
        |
        v
Document Upload, Processing
and Search
```

## Technologies Used

- Microsoft Azure Virtual Machine
- Ubuntu Server 24.04 LTS
- Docker Engine
- Docker Compose
- Paperless-ngx
- PostgreSQL
- Redis
- SSH

## Features Implemented

- Deployed an Ubuntu virtual machine on Azure.
- Connected to the VM using SSH.
- Installed Docker Engine and Docker Compose.
- Configured Paperless-ngx, PostgreSQL, and Redis using Docker Compose.
- Configured persistent Docker volumes and document directories.
- Created a Paperless administrator account.
- Accessed the Paperless web interface through a browser.
- Uploaded a sample PDF document.
- Verified document processing and text search.

## Repository Structure

```text
paperless-ngx/
├── README.md
├── documentation/
│   ├── 01-vm-setup.md
│   ├── 02-docker-installation.md
│   ├── 03-paperless-deployment.md
│   ├── 04-paperless-configuration.md
│   └── 05-verification.md
└── images/
    ├── 01-vm.png
    ├── 02-docker.png
    ├── 03-docker-compose.png
    ├── 04-containers.png
    ├── 05-paperless-login.png
    └── 06-paperless-dashboard.png
```

## Screenshots

### 1. Azure Virtual Machine

![Azure VM](images/01-vm.png)

### 2. Docker Installation

![Docker Installation](images/02-docker.png)

### 3. Docker Compose Configuration

![Docker Compose Configuration](images/03-docker-compose.png)

### 4. Running Containers

![Running Containers](images/04-containers.png)

### 5. Paperless Login

![Paperless Login](images/05-paperless-login.png)

### 6. Paperless Dashboard

![Paperless Dashboard](images/06-paperless-dashboard.png)

## Implementation Documentation

Detailed implementation steps are available in the following documents:

1. [Azure VM Setup](documentation/01-vm-setup.md)
2. [Docker Installation](documentation/02-docker-installation.md)
3. [Paperless Deployment](documentation/03-paperless-deployment.md)
4. [Paperless Configuration](documentation/04-paperless-configuration.md)
5. [Verification](documentation/05-verification.md)

## Accessing the Application

The Paperless-ngx web interface was accessed using:

```text
http://<AZURE-VM-PUBLIC-IP>:8000
```

Replace the placeholder with the public IP address of the Azure VM.

## Project Outcome

Paperless-ngx was deployed on an Azure Ubuntu virtual machine using Docker Compose. The application was accessed through its web interface, and a sample document was uploaded and searched successfully.

This project provided practical experience with cloud VM deployment, Linux administration, Docker containerization, service configuration, and document management.

## Security Note

Environment files containing passwords and secret keys are not included in this repository. No private SSH keys or sensitive documents should be committed.

