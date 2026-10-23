
# 01 - Azure Virtual Machine Setup

## Objective

Create an Azure Virtual Machine to host the Paperless-ngx application.

## Configuration

- Cloud Provider: Microsoft Azure
- Operating System: Ubuntu Server 24.04 LTS
- Access Method: SSH
- Authentication: SSH public key
- Application Port: 8000

## Steps Performed

### 1. Create the Virtual Machine

1. Open the Azure Portal.
2. Navigate to Virtual Machines.
3. Create a new virtual machine.
4. Select Ubuntu Server 24.04 LTS.
5. Configure the VM size and authentication method.
6. Configure networking and the required inbound access.
7. Review the configuration and create the VM.

### 2. Connect Using SSH

From the local computer, connect to the VM using SSH:

```bash
ssh -i "/path/to/private-key.pem" azureuser@<VM-PUBLIC-IP>
```

Replace the private key path, username, and public IP with the values used during VM creation.

### 3. Verify the Operating System

Run the following commands after connecting:

```bash
whoami
hostname
pwd
cat /etc/os-release
```

### 4. Inspect System Resources

```bash
nproc
free -h
df -h
ip -brief address
```

These commands display CPU availability, memory, disk usage, and network interfaces.

## Result

The Azure virtual machine was created and accessed successfully through SSH. Ubuntu was prepared for the Docker installation and application deployment.
