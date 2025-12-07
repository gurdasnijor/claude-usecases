# API Documentation Generator - Quick Start

## Generate OpenAPI Spec

```
Generate OpenAPI 3.1 spec for:
[paste API code or describe endpoints]
```

---

## OpenAPI Structure

```yaml
openapi: 3.1.0
info:
  title: API Name
  version: 1.0.0
servers:
  - url: https://api.example.com/v1
paths:
  /resource:
    get:
      summary: List resources
      responses:
        '200':
          description: Success
components:
  schemas:
    Resource:
      type: object
```

---

## Endpoint Template

```yaml
/resource:
  post:
    summary: Create resource
    description: Detailed description
    tags: [Resources]
    requestBody:
      required: true
      content:
        application/json:
          schema:
            $ref: '#/components/schemas/Input'
    responses:
      '201':
        description: Created
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/Resource'
      '400':
        $ref: '#/components/responses/ValidationError'
```

---

## Schema Template

```yaml
components:
  schemas:
    User:
      type: object
      required: [id, email]
      properties:
        id:
          type: string
          example: "usr_123"
        email:
          type: string
          format: email
        name:
          type: string
          maxLength: 100
```

---

## Common Types

| Type | Format | Example |
|------|--------|---------|
| string | - | "text" |
| string | email | "a@b.com" |
| string | date-time | "2024-01-01T00:00:00Z" |
| string | uuid | "550e8400-..." |
| integer | int32 | 42 |
| number | float | 3.14 |
| boolean | - | true |
| array | - | [...] |
| object | - | {...} |

---

## Auth Schemes

```yaml
components:
  securitySchemes:
    bearerAuth:
      type: http
      scheme: bearer
    apiKey:
      type: apiKey
      in: header
      name: X-API-Key
```

---

## Markdown Reference

```markdown
### POST /users

Create a new user.

**Request:**
| Field | Type | Required |
|-------|------|----------|
| email | string | Yes |

**Response (201):**
```json
{ "id": "usr_123" }
```

**Errors:**
| Code | Description |
|------|-------------|
| 400 | Invalid input |
```

---

## Checklist

- [ ] All endpoints documented
- [ ] Schemas have examples
- [ ] Auth documented
- [ ] Errors included
- [ ] Valid OpenAPI syntax
