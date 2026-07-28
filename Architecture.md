# Architecture

## Overview

This document describes the high-level architecture of the AWS Todo List application.

The application follows a client-server architecture. The frontend is built with React, the backend is implemented with FastAPI, and data is stored in PostgreSQL. All services run inside Docker containers on an AWS EC2 instance behind an Nginx reverse proxy. Deployment is automated using GitHub Actions.

---

# 1. Component Diagram

The application consists of the following components:

- User
- Browser
- React Frontend
- Nginx Reverse Proxy
- FastAPI Backend
- SQLAlchemy ORM
- PostgreSQL Database

```
                User
                  │
                  ▼
          Browser (React)
                  │
               HTTPS
                  │
                  ▼
        Nginx Reverse Proxy
          │             │
          │             ▼
          │       React Static Files
          │
          ▼
      FastAPI Backend
          │
      SQLAlchemy ORM
          │
          ▼
      PostgreSQL
```

### Responsibilities

| Component | Responsibility |
|-----------|----------------|
| React | User interface and API communication |
| Nginx | Serves React files and proxies API requests |
| FastAPI | Business logic and REST API |
| SQLAlchemy | Database abstraction layer |
| PostgreSQL | Persistent data storage |

---

# 2. Deployment Diagram

The application is deployed on an AWS EC2 instance.

GitHub Actions automatically deploys the application after every push to the main branch.

```
GitHub
    │
GitHub Actions
    │
SSH
    │
AWS EC2 (Ubuntu)
┌─────────────────────────────┐
│ Docker Compose              │
│                             │
│  ├── Nginx                  │
│  ├── React                  │
│  ├── FastAPI                │
│  └── PostgreSQL             │
└─────────────────────────────┘
```

Deployment workflow:

```
git push
      │
      ▼
GitHub Actions
      │
      ▼
SSH into EC2
      │
      ▼
docker compose pull
      │
      ▼
docker compose up -d
```

---

# 3. Request / Data Flow

The following diagram illustrates how an HTTP request travels through the system.

```
Browser
    │
GET /
    │
    ▼
Nginx
    │
    ▼
React Application
    │
GET /api/tasks
    │
    ▼
FastAPI
    │
SQLAlchemy
    │
    ▼
PostgreSQL
    │
JSON Response
    │
    ▼
React
    │
Updated UI
```

---

# Architectural Decisions

The following architectural decisions were made during the design phase.

- Client-server architecture
- REST API communication
- React for frontend
- FastAPI for backend
- PostgreSQL as the primary database
- SQLAlchemy as ORM
- Docker Compose for container orchestration
- Nginx as reverse proxy
- AWS EC2 for hosting
- GitHub Actions for CI/CD
- HTTPS for secure communication

---

# Technology Stack

| Layer | Technology |
|--------|------------|
| Frontend | React |
| Backend | FastAPI |
| Database | PostgreSQL |
| ORM | SQLAlchemy |
| Reverse Proxy | Nginx |
| Containers | Docker Compose |
| Hosting | AWS EC2 |
| CI/CD | GitHub Actions |
| Version Control | Git + GitHub |
