# Deployment

## Overview

This document describes the deployment architecture of the AWS Todo Cloud application.

The application is deployed on an AWS EC2 virtual machine using Docker Compose.

Deployment is automated through GitHub Actions.

---

# Deployment Environment

| Component | Technology |
|------------|------------|
| Cloud Provider | AWS |
| Virtual Machine | EC2 |
| Operating System | Ubuntu Server |
| Containers | Docker |
| Container Orchestration | Docker Compose |
| Reverse Proxy | Nginx |
| CI/CD | GitHub Actions |
| Version Control | GitHub |

---

# Production Architecture

```
Internet
     │
     ▼
 HTTPS (443)
     │
     ▼
AWS EC2
│
├── Nginx
│
├── React Frontend
│
├── FastAPI Backend
│
└── PostgreSQL
```

All application services run inside Docker containers.

---

# Docker Containers

The production environment contains the following containers.

| Container | Responsibility |
|------------|----------------|
| nginx | Reverse proxy and HTTPS |
| frontend | React application |
| backend | FastAPI application |
| postgres | PostgreSQL database |

---

# Deployment Workflow

The application is deployed automatically after code is pushed to the main branch.

```
Developer

↓

git push

↓

GitHub Repository

↓

GitHub Actions

↓

Build Docker Images

↓

SSH Connection

↓

AWS EC2

↓

docker compose pull

↓

docker compose up -d
```

---

# Application Flow

```
User

↓

Browser

↓

HTTPS

↓

Nginx

↓

React

↓

REST API

↓

FastAPI

↓

SQLAlchemy

↓

PostgreSQL
```

---

# Reverse Proxy

Nginx is responsible for:

- HTTPS termination
- Reverse proxy
- Routing requests
- Serving frontend files
- Forwarding API requests to FastAPI

---

# Docker Compose

Docker Compose manages all application services.

Services include:

- frontend
- backend
- postgres
- nginx

Docker Compose provides:

- service networking
- container management
- persistent storage
- simplified deployment

---

# Persistent Storage

The PostgreSQL database uses a Docker Volume.

```
Docker Volume

↓

PostgreSQL

↓

Persistent Data
```

This ensures that application data remains available after container restarts.

---

# Environment Variables

Sensitive configuration values are stored as environment variables.

Examples include:

- Database credentials
- JWT secret key
- Database URL
- Application environment
- API configuration

Environment variables are not stored inside the source code repository.

---

# HTTPS

Communication between users and the application is encrypted using HTTPS.

Benefits include:

- encrypted communication
- secure authentication
- secure JWT transmission
- data integrity

---

# CI/CD Pipeline

GitHub Actions automates deployment.

Pipeline steps:

1. Detect changes in the repository.
2. Build the application.
3. Connect to AWS EC2 using SSH.
4. Pull the latest changes.
5. Restart Docker containers.
6. Verify successful deployment.

---

# Deployment Requirements

Production server requirements:

- Ubuntu Server
- Docker
- Docker Compose
- Git
- Nginx
- Internet access
- SSH access

---

# Security

Deployment security includes:

- HTTPS encryption
- SSH authentication
- JWT authentication
- Password hashing
- Environment variables
- Docker network isolation

---

# Future Improvements

Possible future enhancements include:

- Amazon RDS instead of local PostgreSQL
- Amazon ECS
- Kubernetes
- Automatic SSL certificate renewal
- Monitoring with Prometheus
- Grafana dashboards
- Log aggregation
- Horizontal scaling
- Load balancing
- Automatic backups
