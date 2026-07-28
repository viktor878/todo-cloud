# Database Design

## Overview

The application uses PostgreSQL as the primary relational database.

Database access is implemented using SQLAlchemy ORM. Each registered user owns their own tasks. Authentication is based on JSON Web Tokens (JWT).

---

# Database Technology

| Component | Technology |
|-----------|------------|
| Database | PostgreSQL |
| ORM | SQLAlchemy |
| Migration Tool | Alembic *(planned)* |

---

# Entity Relationship Diagram

The application contains two main entities.

```
+----------------+          +----------------+
|     User       |          |      Task      |
+----------------+          +----------------+
| id             |<------┐  | id             |
| username       |       │  | user_id (FK)   |
| email          |       └──| title          |
| password_hash  |          | completed      |
| created_at     |          | created_at     |
+----------------+          | updated_at     |
                            +----------------+
```

Relationship:

```
One User
     │
     └──────────────► Many Tasks
```

Each task belongs to exactly one user.

---

# Table: users

The `users` table stores registered users.

| Column | Type | Description |
|---------|------|-------------|
| id | UUID | Primary key |
| username | VARCHAR | Username |
| email | VARCHAR | User email |
| password_hash | VARCHAR | Hashed password |
| created_at | TIMESTAMP | Account creation date |

---

# Table: tasks

The `tasks` table stores todo items.

| Column | Type | Description |
|---------|------|-------------|
| id | UUID | Primary key |
| user_id | UUID | Foreign key to users.id |
| title | VARCHAR | Task title |
| completed | BOOLEAN | Completion status |
| created_at | TIMESTAMP | Creation date |
| updated_at | TIMESTAMP | Last update date |

---

# Relationships

```
users
   │
   │ 1
   │
   ▼
tasks
   ▲
   │ *
```

Relationship type:

- One User → Many Tasks

Every task belongs to exactly one user.

---

# Data Validation

The backend validates all incoming data before writing it to the database.

User validation:

- username is required
- email is required
- email must be unique
- password is stored only as a hash
- password must satisfy minimum security requirements

Task validation:

- title is required
- title cannot be empty
- title length is limited
- completed accepts only boolean values
- user_id is assigned automatically
- timestamps are generated automatically

---

# Database Access

The application communicates with the database through SQLAlchemy ORM.

```
FastAPI

↓

SQLAlchemy ORM

↓

PostgreSQL
```

Business logic never communicates directly with PostgreSQL using raw SQL.

---

# Authentication Data

Passwords are never stored in plain text.

The application stores only password hashes.

Authentication is implemented using JWT.

Typical authentication flow:

```
User Login

↓

Password Verification

↓

JWT Token

↓

Authenticated Requests

↓

Database Access
```

---

# Persistence

PostgreSQL runs inside a Docker container.

Database files are stored inside a Docker Volume to ensure persistence after container restarts.

```
Docker Volume

↓

PostgreSQL

↓

Persistent Storage
```

---

# Future Improvements

Possible future enhancements include:

- Task categories
- Task priorities
- Due dates
- File attachments
- Soft delete
- Refresh Tokens
- Email verification
- Password reset
- Database indexing optimization
- Alembic database migrations
