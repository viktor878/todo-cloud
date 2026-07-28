# API Documentation

## Overview

The application exposes a RESTful API for user authentication and task management.

The API is implemented using FastAPI and communicates via JSON over HTTPS.

Authentication is based on JSON Web Tokens (JWT).

---

# Base URL

Development

```
http://localhost:8000/api
```

Production

```
https://todo.example.com/api
```

---

# API Principles

- REST architecture
- JSON request and response format
- Stateless communication
- JWT authentication
- Standard HTTP status codes

---

# Authentication

Most endpoints require a valid JWT access token.

Example request header

```
Authorization: Bearer <access_token>
```

---

# Authentication Endpoints

## Register

Creates a new user account.

### Request

```
POST /auth/register
```

Request Body

```json
{
    "username": "john",
    "email": "john@example.com",
    "password": "StrongPassword123"
}
```

Response

```json
{
    "message": "User created successfully"
}
```

Status Codes

| Code | Description |
|------|-------------|
| 201 | User created |
| 400 | Validation error |
| 409 | User already exists |

---

## Login

Authenticates a user and returns a JWT access token.

### Request

```
POST /auth/login
```

Request Body

```json
{
    "email": "john@example.com",
    "password": "StrongPassword123"
}
```

Response

```json
{
    "access_token": "<jwt_token>",
    "token_type": "bearer"
}
```

Status Codes

| Code | Description |
|------|-------------|
| 200 | Success |
| 401 | Invalid credentials |

---

## Current User

Returns information about the authenticated user.

### Request

```
GET /users/me
```

Response

```json
{
    "id": "uuid",
    "username": "john",
    "email": "john@example.com"
}
```

Status Codes

| Code | Description |
|------|-------------|
| 200 | Success |
| 401 | Unauthorized |

---

# Task Endpoints

## Get All Tasks

Returns all tasks belonging to the authenticated user.

### Request

```
GET /tasks
```

Response

```json
[
    {
        "id": "uuid",
        "title": "Learn AWS",
        "completed": false,
        "created_at": "2026-07-28T14:00:00Z",
        "updated_at": "2026-07-28T14:00:00Z"
    }
]
```

Status Codes

| Code | Description |
|------|-------------|
| 200 | Success |
| 401 | Unauthorized |

---

## Get Task

Returns a single task.

### Request

```
GET /tasks/{id}
```

Response

```json
{
    "id": "uuid",
    "title": "Learn AWS",
    "completed": false,
    "created_at": "2026-07-28T14:00:00Z",
    "updated_at": "2026-07-28T14:00:00Z"
}
```

Status Codes

| Code | Description |
|------|-------------|
| 200 | Success |
| 401 | Unauthorized |
| 404 | Task not found |

---

## Create Task

Creates a new task.

### Request

```
POST /tasks
```

Request Body

```json
{
    "title": "Learn Docker"
}
```

Response

```json
{
    "id": "uuid",
    "title": "Learn Docker",
    "completed": false,
    "created_at": "2026-07-28T14:00:00Z",
    "updated_at": "2026-07-28T14:00:00Z"
}
```

Status Codes

| Code | Description |
|------|-------------|
| 201 | Created |
| 400 | Validation error |
| 401 | Unauthorized |

---

## Update Task

Updates an existing task.

### Request

```
PUT /tasks/{id}
```

Request Body

```json
{
    "title": "Learn FastAPI",
    "completed": true
}
```

Response

```json
{
    "id": "uuid",
    "title": "Learn FastAPI",
    "completed": true,
    "created_at": "2026-07-28T14:00:00Z",
    "updated_at": "2026-07-28T15:10:00Z"
}
```

Status Codes

| Code | Description |
|------|-------------|
| 200 | Success |
| 400 | Validation error |
| 401 | Unauthorized |
| 404 | Task not found |

---

## Delete Task

Deletes a task.

### Request

```
DELETE /tasks/{id}
```

Response

```
204 No Content
```

Status Codes

| Code | Description |
|------|-------------|
| 204 | Deleted |
| 401 | Unauthorized |
| 404 | Task not found |

---

# Task Model

```json
{
    "id": "uuid",
    "title": "Learn AWS",
    "completed": false,
    "created_at": "2026-07-28T14:00:00Z",
    "updated_at": "2026-07-28T14:00:00Z"
}
```

---

# User Model

```json
{
    "id": "uuid",
    "username": "john",
    "email": "john@example.com"
}
```

---

# Validation Rules

User

- username is required
- email is required
- email must be unique
- password must meet minimum security requirements

Task

- title is required
- title cannot be empty
- completed accepts only boolean values

---

# HTTP Status Codes

| Code | Meaning |
|------|---------|
| 200 | OK |
| 201 | Created |
| 204 | No Content |
| 400 | Bad Request |
| 401 | Unauthorized |
| 404 | Not Found |
| 409 | Conflict |
| 500 | Internal Server Error |

---

# Interactive API Documentation

FastAPI automatically generates API documentation.

Swagger UI

```
http://localhost:8000/docs
```

ReDoc

```
http://localhost:8000/redoc
```
