# API Documentation

## Overview

The application exposes a REST API that allows clients to create, read, update, and delete todo tasks.

The API is implemented using FastAPI and communicates using JSON over HTTP.

Base URL:

```
http://localhost:8000/api
```

Production:

```
https://todo.example.com/api
```

---

# API Principles

- RESTful architecture
- JSON request and response format
- Stateless communication
- Standard HTTP status codes

---

# Endpoints

## Get all tasks

Returns a list of all tasks.

### Request

```
GET /tasks
```

### Response

```json
[
  {
    "id": 1,
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

---

## Get task by ID

Returns a single task.

### Request

```
GET /tasks/{id}
```

Example

```
GET /tasks/1
```

### Response

```json
{
  "id": 1,
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
| 404 | Task not found |

---

## Create task

Creates a new task.

### Request

```
POST /tasks
```

Request Body

```json
{
  "title": "Learn AWS"
}
```

### Response

```json
{
  "id": 1,
  "title": "Learn AWS",
  "completed": false,
  "created_at": "2026-07-28T14:00:00Z",
  "updated_at": "2026-07-28T14:00:00Z"
}
```

Status Codes

| Code | Description |
|------|-------------|
| 201 | Created |
| 400 | Invalid request |

---

## Update task

Updates an existing task.

### Request

```
PUT /tasks/{id}
```

Request Body

```json
{
  "title": "Learn Docker",
  "completed": true
}
```

### Response

```json
{
  "id": 1,
  "title": "Learn Docker",
  "completed": true,
  "created_at": "2026-07-28T14:00:00Z",
  "updated_at": "2026-07-28T15:20:00Z"
}
```

Status Codes

| Code | Description |
|------|-------------|
| 200 | Success |
| 404 | Task not found |

---

## Delete task

Deletes a task.

### Request

```
DELETE /tasks/{id}
```

Example

```
DELETE /tasks/1
```

### Response

```
204 No Content
```

Status Codes

| Code | Description |
|------|-------------|
| 204 | Deleted successfully |
| 404 | Task not found |

---

# HTTP Status Codes

| Code | Meaning |
|------|---------|
| 200 | OK |
| 201 | Created |
| 204 | No Content |
| 400 | Bad Request |
| 404 | Not Found |
| 500 | Internal Server Error |

---

# Data Model

```json
{
  "id": 1,
  "title": "Learn AWS",
  "completed": false,
  "created_at": "2026-07-28T14:00:00Z",
  "updated_at": "2026-07-28T14:00:00Z"
}
```

---

# Validation Rules

- `title` is required
- `title` cannot be empty
- `title` has a maximum length limit
- `completed` accepts only boolean values
- `id` is generated automatically
- `created_at` is generated automatically
- `updated_at` is updated automatically

---

# Authentication

The current version of the application does not require authentication.

Authentication (JWT or AWS Cognito) is planned for future releases.

---

# Interactive Documentation

FastAPI automatically generates interactive API documentation.

Swagger UI:

```
http://localhost:8000/docs
```

ReDoc:

```
http://localhost:8000/redoc
```
