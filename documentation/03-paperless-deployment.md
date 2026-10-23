
# 03 - Paperless-ngx Deployment

## Objective

Deploy Paperless-ngx and its supporting services on the Azure VM using Docker Compose.

## 1. Create the Project Directory

```bash
sudo mkdir -p /opt/paperless
sudo chown "$USER":"$USER" /opt/paperless
cd /opt/paperless
```

Create the document import and export directories:

```bash
mkdir -p consume export
```

The project files are stored in `/opt/paperless`.

## 2. Create the Environment File

Generate the secret values used by the deployment:

```bash
cat > .env <<EOF
POSTGRES_PASSWORD=$(openssl rand -hex 24)
PAPERLESS_SECRET_KEY=$(openssl rand -hex 32)
EOF
```

Restrict access to the environment file:

```bash
chmod 600 .env
```

The environment file contains the PostgreSQL password and Paperless secret key.

It should not be uploaded to GitHub.

## 3. Configure Docker Compose

Create the Compose file:

```bash
nano docker-compose.yml
```

The deployment contains three services:

- `webserver`: Paperless-ngx application.
- `db`: PostgreSQL database.
- `broker`: Redis service.

The Compose configuration defines the images, environment variables, port mapping, service dependencies, and persistent storage.

The complete configuration is documented in `04-paperless-configuration.md`.

## 4. Validate the Configuration

```bash
docker compose config -q
```

This checks whether Docker Compose can parse and resolve the configuration.

## 5. Download the Images

```bash
sudo docker compose pull
```

This downloads the container images specified in the Compose file.

## 6. Start the Services

```bash
sudo docker compose up -d
```

The `-d` option starts the services in the background.

## 7. Verify the Deployment

```bash
sudo docker compose ps
```

Inspect the application logs:

```bash
sudo docker compose logs --tail=50
```

The deployment uses Docker Compose to manage Paperless-ngx, PostgreSQL, and Redis as one application.

## 8. Create the Administrator Account

```bash
sudo docker compose exec webserver createsuperuser
```

Follow the prompts to create the Paperless administrator account.

## 9. Access the Application

Open the following address in a browser:

```text
http://<AZURE-VM-PUBLIC-IP>:8000
```

Replace the placeholder with the Azure VM's public IP address.

The application is accessed through the mapped host port 8000.

## Result

Paperless-ngx and its supporting services were deployed using Docker Compose. The administrator account was created, and the application was accessed through a web browser.
