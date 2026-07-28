# Database Design

## Overview

The application uses PostgreSQL as the primary relational database.

The database stores user tasks and provides persistent storage for the backend application. Database access is implemented through SQLAlchemy ORM.

---

# Database Technology

| Component | Technology |
|-----------|------------|
| Database | PostgreSQL |
| ORM | SQLAlchemy |
| Migration Tool | Alembic *(planned)* |

---

# Entity Relationship Diagram

The current version of the application contains a single entity.

```
+----------------------------------+
|              Task                |
+----------------------------------+
| id              UUID / Integer   |
| title           VARCHAR          |
| completed       BOOLEAN          |
| created_at      TIMESTAMP        |
| updated_at      TIMESTAMP        |
+----------------------------------+
```

Future versions may introduce additional entities such as User, Category, or Labels.

---

# Table: tasks

The `tasks` table stores all todo items.

| Column | Type | Description |
|---------|------|-------------|
| id | UUID / Integer | Primary key |
| title | VARCHAR | Task title |
| completed | BOOLEAN | Completion status |
| created_at | TIMESTAMP | Creation date |
| updated_at | TIMESTAMP | Last update date |

---

# Relationships

Current version:

```
Task
```

There are no foreign keys in the initial version of the application.

Future versions may include:

```
User
   │
   └──────────────┐
                  │
                Task
```

where one user can own multiple tasks.

---

# Data Validation

The backend validates all incoming data before writing it to the database.

Validation rules include:

- title must not be empty
- title length is limited
- completed accepts only boolean values
- id is generated automatically
- timestamps are generated automatically

---

# Database Access

The application interacts with the database through SQLAlchemy ORM.

Application flow:

```
FastAPI

↓

SQLAlchemy ORM

↓

PostgreSQL
```

Direct SQL queries are not used in the application code.

---

# Persistence

PostgreSQL runs inside a Docker container.

Database files are stored in a Docker volume to ensure that data persists after container restarts.

```
Docker Volume

↓

PostgreSQL

↓

Persistent Storage
```

---

# Future Improvements

Planned database enhancements include:

- User accounts
- Authentication
- Task categories
- Task priorities
- Due dates
- Soft delete
- Index optimization
- Database migrations with Alembic
