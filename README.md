# Linux, Networking & Cloud Infrastructure

## About

This repository contains my work for Module 2 of my internship. In this module, I worked with Linux, AWS EC2, networking, SSH, security groups, and Nginx.

## Topics Covered

- Linux command-line basics
- Files and permissions
- Users and groups
- Processes and services
- SSH
- IP addressing
- DNS
- Ports
- Firewalls
- AWS Security Groups
- EC2 Linux server deployment

## Tools Used

- AWS EC2
- Amazon Linux 2023
- Windows PowerShell
- SSH
- Nginx

## Practical Work

### 1. Created Linux Server

Created an Amazon EC2 instance using:

- Amazon Linux 2023
- t3.micro
- 8 GiB gp3 storage
- Public IPv4 address

### 2. Connected Using SSH

Connected to the EC2 Linux server from Windows PowerShell using an SSH key pair.

### 3. Configured Security

Configured the EC2 Security Group with:

- SSH – My IP
- HTTP – Anywhere

### 4. Deployed Nginx

Installed and started the Nginx web server using:

```bash
sudo dnf install nginx -y
sudo systemctl start nginx
sudo systemctl enable nginx
sudo systemctl status nginx

The Nginx service was successfully running.

5. Tested Connectivity

Opened the EC2 public IP address in a web browser and verified that the Nginx welcome page was displayed.

Deployment Flow

Create EC2 Instance
↓
Configure Linux
↓
Connect using SSH
↓
Configure Security Group
↓
Install Nginx
↓
Start Nginx
↓
Test Connectivity

Result

Successfully created and configured a Linux server on AWS EC2, connected to it using SSH, deployed Nginx, and tested the web server through its public IP.

Screenshots

Screenshots of the practical work are available in the screenshots folder.
