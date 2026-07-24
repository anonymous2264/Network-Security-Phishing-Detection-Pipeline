# 🚀 Deployment Guide

This guide explains how to configure AWS credentials, GitHub Secrets, Amazon ECR, and an EC2 instance to automate the deployment of the **Network Security - Phishing Detection** project using GitHub Actions and Docker.

---

# Prerequisites

Before starting, ensure you have:

- An AWS Account
- An EC2 Ubuntu Instance
- An Amazon ECR Repository
- Docker Installed (or install using the steps below)
- A GitHub Repository

---

# GitHub Secrets Configuration

Navigate to:

```
Repository
    ├── Settings
    ├── Secrets and Variables
    ├── Actions
    └── New Repository Secret
```

Create the following secrets:

| Secret Name | Description |
|-------------|-------------|
| `AWS_ACCESS_KEY_ID` | AWS IAM Access Key |
| `AWS_SECRET_ACCESS_KEY` | AWS IAM Secret Access Key |
| `AWS_REGION` | AWS Region (e.g. `us-east-1`) |
| `AWS_ECR_LOGIN_URI` | Amazon ECR Login URI |
| `ECR_REPOSITORY_NAME` | Name of the ECR Repository |

Example:

```text
AWS_REGION=us-east-1

AWS_ECR_LOGIN_URI=788614365622.dkr.ecr.us-east-1.amazonaws.com

ECR_REPOSITORY_NAME=networkssecurity
```

---

# EC2 Setup

Connect to your Ubuntu EC2 instance via SSH.

## Update Packages

```bash
sudo apt-get update -y
sudo apt-get upgrade -y
```

---

## Install Docker

Download the official Docker installation script

```bash
curl -fsSL https://get.docker.com -o get-docker.sh
```

Install Docker

```bash
sudo sh get-docker.sh
```

Verify installation

```bash
docker --version
```

---

## Configure Docker Permissions

Allow the Ubuntu user to run Docker commands without `sudo`.

```bash
sudo usermod -aG docker ubuntu
```

Refresh group permissions

```bash
newgrp docker
```

Verify

```bash
docker ps
```

---

# Deployment Workflow

```
Developer
      │
      ▼
Push Code to GitHub
      │
      ▼
GitHub Actions
      │
      ▼
Build Docker Image
      │
      ▼
Push Image to Amazon ECR
      │
      ▼
EC2 Instance
      │
      ▼
Pull Latest Docker Image
      │
      ▼
Run Container
      │
      ▼
Network Security Application
```

---

# Technologies Used

- Python
- Docker
- GitHub Actions
- AWS EC2
- Amazon ECR
- AWS IAM
- Ubuntu Linux

---

# Notes

- Never commit AWS credentials to the repository.
- Store all sensitive information using GitHub Secrets.
- Ensure the IAM user has permissions to access Amazon ECR.
- Verify Docker is installed and running before deploying.
