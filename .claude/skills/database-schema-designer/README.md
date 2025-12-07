# Database Schema Designer

> Design optimized schemas, queries, and migrations for SQL and NoSQL databases

## Overview

The Database Schema Designer creates robust, scalable database schemas. It provides guidance on normalization, indexing strategies, query optimization, and migrations across SQL and NoSQL databases.

## When to Use

- **Design new database schemas** from requirements
- **Normalize or denormalize** existing schemas
- **Create migrations** safely
- **Optimize queries** for performance
- **Design indexes** strategically
- **Model MongoDB schemas** with embedding/referencing decisions

## Supported Databases

| Type | Databases |
|------|-----------|
| **SQL** | PostgreSQL, MySQL, SQLite, SQL Server |
| **NoSQL** | MongoDB, Redis, DynamoDB, Cassandra |

## Quick Example

**Input:**
```
Design a schema for a blog with users, posts, comments, and tags.
```

**Generated Schema:**
```sql
CREATE TABLE users (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    email VARCHAR(255) NOT NULL UNIQUE,
    name VARCHAR(100) NOT NULL,
    created_at TIMESTAMPTZ DEFAULT NOW()
);

CREATE TABLE posts (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    user_id UUID REFERENCES users(id) ON DELETE CASCADE,
    title VARCHAR(255) NOT NULL,
    content TEXT,
    status VARCHAR(20) DEFAULT 'draft',
    created_at TIMESTAMPTZ DEFAULT NOW()
);

CREATE INDEX idx_posts_user_id ON posts(user_id);
CREATE INDEX idx_posts_status ON posts(status);
```

## Key Capabilities

| Capability | Description |
|------------|-------------|
| **Schema Design** | Tables, relationships, constraints |
| **Normalization** | 1NF, 2NF, 3NF guidance |
| **Indexing** | B-tree, GIN, partial, composite |
| **Query Optimization** | EXPLAIN ANALYZE, N+1 prevention |
| **Migrations** | Safe patterns, rollback support |
| **NoSQL** | MongoDB embedding vs referencing |

## Relationship Patterns

- **1:N** - Foreign key on child table
- **N:M** - Junction/join table
- **1:1** - FK on either table or embed
- **Self-referential** - Parent/child hierarchy

## Index Guidelines

| Query Pattern | Index Type |
|---------------|------------|
| Equality (=) | B-tree |
| Range (<, >) | B-tree |
| JSONB queries | GIN |
| Full-text search | GIN/GiST |
| Partial data | Partial index |

## Usage

**Design schema:**
```
Design a PostgreSQL schema for an e-commerce application with:
- Users and authentication
- Products with categories
- Orders with line items
- Reviews
```

**Optimize query:**
```
Optimize this query:
SELECT * FROM orders WHERE status = 'pending' ORDER BY created_at;
```

**Create migration:**
```
Create a safe migration to add a 'phone' column to users table.
```

## Related Skills

- **api-documentation-generator** - Document data models
- **code-review-assistant** - Review SQL security
- **technical-writer** - Database documentation

## Version

- **Current:** v1.0.0
- **Last Updated:** 2025-12-07
- **Author:** 360 Social Impact Studios
