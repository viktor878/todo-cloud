# Architecture

## Overview

This document describes the high-level architecture of the AWS Todo Cloud application.

The application follows a client-server architecture. The frontend is built with React, the backend is implemented using FastAPI, and PostgreSQL is used for persistent data storage.

Authentication is implemented using JSON Web Tokens (JWT).

All application components run inside Docker containers on an AWS EC2 instance behind an Nginx reverse proxy.

Deployment is automated using GitHub Actions.

---

# Architecture Style

The application follows:

- Client-Server Architecture
- REST API
- Layered Architecture
- Stateless Authentication (JWT)

---

# System Components

| Component | Responsibility |
|------------|----------------|
| React | User Interface |
| Nginx | Reverse Proxy and Static File Server |
| FastAPI | REST API and Business Logic |
| JWT Authentication | User Authentication |
| SQLAlchemy | ORM |
| PostgreSQL | Persistent Storage |
| Docker Compose | Container Orchestration |
| GitHub Actions | Continuous Deployment |
| AWS EC2 | Application Hosting |

---

# Component Diagram

The following diagram illustrates the logical architecture of the application.

```
                          User
                            │
                            ▼
                     Web Browser
                            │
                         HTTPS
                            │
                            ▼
                 Nginx Reverse Proxy
                 ┌──────────┴──────────┐
                 │                     │
                 ▼                     ▼
          React Frontend        FastAPI Backend
                                      │
                     ┌────────────────┴────────────────┐
                     │                                 │
                     ▼                                 ▼
             JWT Authentication               Task Service
                     │                                 │
                     └────────────────┬────────────────┘
                                      ▼
                                SQLAlchemy ORM
                                      │
                                      ▼
                                PostgreSQL
```

---

# Deployment Diagram

The application is deployed on a single AWS EC2 instance.

```
GitHub
    │
    ▼
GitHub Actions
    │
SSH Deployment
    │
    ▼
AWS EC2 (Ubuntu)

┌────────────────────────────────────────────┐
│ Docker Compose                             │
│                                            │
│ ┌────────────┐                             │
│ │   Nginx    │                             │
│ └─────┬──────┘                             │
│       │                                    │
│ ┌─────▼──────┐   ┌──────────────────────┐  │
│ │ React App  │   │ FastAPI Backend      │  │
│ └────────────┘   └──────────┬───────────┘  │
│                             │              │
│                     ┌────────▼────────┐    │
│                     │ PostgreSQL      │    │
│                     └─────────────────┘    │
└────────────────────────────────────────────┘
```

Deployment workflow:

```
Developer

↓

git push

↓

GitHub Repository

↓

GitHub Actions

↓

SSH

↓

AWS EC2

↓

docker compose pull

↓

docker compose up -d
```

---

# Request Flow

The following diagram illustrates a typical authenticated request.

```
User

↓

Browser

↓

React

↓

POST /auth/login

↓

FastAPI

↓

Password Verification

↓

JWT Access Token

↓

Browser

↓

Authorization: Bearer <token>

↓

GET /tasks

↓

FastAPI

↓

JWT Validation

↓

Task Service

↓

SQLAlchemy

↓

PostgreSQL

↓

JSON Response

↓

React

↓

Updated User Interface
```

---

# Layered Architecture

The backend follows a layered architecture.

```
Presentation Layer
        │
        ▼
REST API (FastAPI)
        │
        ▼
Business Logic
        │
        ▼
SQLAlchemy ORM
        │
        ▼
PostgreSQL
```

---

# Security

Security measures include:

- HTTPS communication
- JWT Authentication
- Password hashing
- Input validation
- ORM protection against SQL Injection
- Authentication middleware
- User authorization

---

# Architectural Decisions

The following architectural decisions were made during the design phase.

- React is used for the frontend.
- FastAPI is used for the backend.
- REST API is used for communication.
- JWT is used for authentication.
- PostgreSQL is used as the relational database.
- SQLAlchemy is used as the ORM.
- Docker Compose is used for container orchestration.
- Nginx acts as the reverse proxy.
- GitHub Actions automates deployment.
- AWS EC2 hosts the production environment.

---

# Technology Stack

| Layer | Technology |
|--------|------------|
| Frontend | React |
| Backend | FastAPI |
| Authentication | JWT |
| ORM | SQLAlchemy |
| Database | PostgreSQL |
| Reverse Proxy | Nginx |
| Containers | Docker Compose |
| CI/CD | GitHub Actions |
| Hosting | AWS EC2 |
| Version Control | Git + GitHub |
