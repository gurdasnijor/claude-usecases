# Database Schema Designer - Quick Start

## Request Schema Design

```
Design a [PostgreSQL/MySQL/MongoDB] schema for:
[describe entities and relationships]
```

---

## Table Template (PostgreSQL)

```sql
CREATE TABLE table_name (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    -- fields
    created_at TIMESTAMPTZ NOT NULL DEFAULT NOW(),
    updated_at TIMESTAMPTZ NOT NULL DEFAULT NOW()
);

CREATE INDEX idx_table_field ON table_name(field);
```

---

## Relationships

**One-to-Many:**
```sql
-- Parent
CREATE TABLE users (id UUID PRIMARY KEY);

-- Child (has FK to parent)
CREATE TABLE posts (
    id UUID PRIMARY KEY,
    user_id UUID REFERENCES users(id) ON DELETE CASCADE
);
```

**Many-to-Many:**
```sql
-- Junction table
CREATE TABLE post_tags (
    post_id UUID REFERENCES posts(id),
    tag_id UUID REFERENCES tags(id),
    PRIMARY KEY (post_id, tag_id)
);
```

---

## Common Data Types

| Type | Use For |
|------|---------|
| UUID | Primary keys |
| VARCHAR(N) | Short text |
| TEXT | Long text |
| INTEGER | Whole numbers |
| DECIMAL(10,2) | Money |
| TIMESTAMPTZ | Dates/times |
| JSONB | Flexible data |
| BOOLEAN | True/false |

---

## Index Quick Reference

```sql
-- Basic index
CREATE INDEX idx_name ON table(column);

-- Composite (multi-column)
CREATE INDEX idx_name ON table(col1, col2);

-- Unique
CREATE UNIQUE INDEX idx_name ON table(column);

-- Partial (filtered)
CREATE INDEX idx_name ON table(col) WHERE status = 'active';

-- JSONB
CREATE INDEX idx_name ON table USING GIN(jsonb_col);
```

---

## Normalization Quick Check

| Form | Rule |
|------|------|
| 1NF | No repeating groups, atomic values |
| 2NF | No partial dependencies |
| 3NF | No transitive dependencies |

---

## Safe Migrations

```sql
-- Add nullable column (safe)
ALTER TABLE users ADD COLUMN phone VARCHAR(20);

-- Add with default (safe)
ALTER TABLE users ADD COLUMN status VARCHAR(20) DEFAULT 'active';

-- Create index without locking
CREATE INDEX CONCURRENTLY idx_name ON table(col);
```

---

## Query Optimization

```sql
-- Check query plan
EXPLAIN ANALYZE SELECT ...;

-- Use LIMIT
SELECT * FROM posts ORDER BY created_at LIMIT 20;

-- Cursor pagination (better than OFFSET)
WHERE created_at < ? ORDER BY created_at LIMIT 20;
```

---

## MongoDB Quick Reference

**Embed:**
```javascript
{ user: { profile: { bio: "..." } } }
```

**Reference:**
```javascript
{ userId: ObjectId("...") }  // Separate collection
```

**Index:**
```javascript
db.collection.createIndex({ field: 1 })
```
