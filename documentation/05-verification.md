
# 05 - Deployment Verification

## Objective

Verify that Paperless-ngx is running and that its document management functionality works as expected.

## 1. Verify Running Containers

Run:

```bash
sudo docker compose ps
```

This displays the status of the services defined in the Compose file.

The deployment includes:

- Paperless-ngx (`webserver`)
- PostgreSQL (`db`)
- Redis (`broker`)

## 2. Check Application Logs

```bash
sudo docker compose logs --tail=50 webserver
```

This displays recent application logs and helps verify that the webserver has started.

## 3. Access the Web Interface

Open the following address in a browser:

```text
http://<AZURE-VM-PUBLIC-IP>:8000
```

Log in using the administrator account created during deployment.

## 4. Verify Document Upload

Upload a sample PDF through the Paperless-ngx web interface.

Wait for the document to finish processing, then open the imported document and check its details.

## 5. Verify Document Search

Search for text contained in the uploaded document.

The search was tested using terms such as `MBA` and `2026` from the sample admission report.

A matching result demonstrates that the document's content can be searched through the Paperless interface.

## 6. Verify Persistent Storage Configuration

Run:

```bash
sudo docker volume ls
```

Inspect the volume mappings of the Paperless container:

```bash
sudo docker inspect "$(sudo docker compose ps -q webserver)" \
  --format '{{range .Mounts}}{{println .Type .Destination}}{{end}}'
```

These commands display the Docker volumes and mount destinations associated with the deployment.

## Verification Summary

The following functionality was verified:

- Paperless-ngx was deployed on the Azure VM.
- The web interface was accessible through a browser.
- The administrator account was created and used to log in.
- A sample PDF was uploaded and processed.
- Document content could be searched.
- Docker volumes and document directory mounts were configured.

## Result

The deployment was verified through the Paperless web interface and command-line checks. Document upload and search functionality worked successfully.
