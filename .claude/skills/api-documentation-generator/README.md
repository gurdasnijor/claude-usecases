# API Documentation Generator

> Generate OpenAPI specs, API references, and SDK documentation from code

## Overview

The API Documentation Generator creates comprehensive API documentation from source code or specifications. It produces OpenAPI/Swagger specs, human-readable references, and SDK documentation.

## When to Use

- **Generate OpenAPI specs** from existing API code
- **Document REST endpoints** with examples
- **Create SDK documentation** for client libraries
- **Build integration guides** for third-party developers

## Output Formats

| Format | Use Case |
|--------|----------|
| **OpenAPI 3.x (YAML/JSON)** | Swagger UI, code generation, tooling |
| **Markdown Reference** | Documentation sites, README |
| **SDK Docs** | Client library usage |
| **Postman Collection** | API testing |

## Quick Example

**Input (Python/FastAPI):**
```python
@app.post("/users")
def create_user(user: CreateUserInput) -> User:
    """Create a new user account."""
    ...
```

**Generated OpenAPI:**
```yaml
paths:
  /users:
    post:
      summary: Create a new user account
      requestBody:
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/CreateUserInput'
      responses:
        '201':
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/User'
```

## What Gets Documented

- Endpoints with methods (GET, POST, PUT, DELETE)
- Request/response schemas with types
- Query, path, and header parameters
- Authentication requirements
- Error codes and responses
- Rate limiting information

## OpenAPI Spec Includes

```yaml
openapi: 3.1.0
info:          # API metadata
servers:       # Base URLs
tags:          # Endpoint grouping
paths:         # All endpoints
components:
  schemas:     # Data models
  securitySchemes:  # Auth methods
  responses:   # Reusable responses
```

## Usage

**Generate full OpenAPI spec:**
```
Generate OpenAPI 3.1 spec for this API:
[paste code or describe endpoints]
```

**Generate markdown reference:**
```
Create API reference documentation for these endpoints:
[paste code]
```

**Generate SDK docs:**
```
Document this JavaScript SDK:
[paste client library code]
```

## Related Skills

- **technical-writer** - Integration guides
- **tool-use-designer** - Claude tool APIs
- **code-review-assistant** - API design review

## Version

- **Current:** v1.0.0
- **Last Updated:** 2025-12-07
- **Author:** 360 Social Impact Studios
