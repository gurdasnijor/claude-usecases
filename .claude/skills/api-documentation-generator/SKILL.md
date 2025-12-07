---
name: API Documentation Generator
description: Generate comprehensive API documentation including OpenAPI/Swagger specifications, endpoint references, SDK documentation, and integration guides from code or specifications
version: 1.0.0
author: 360 Social Impact Studios
created: 2025-12-07
updated: 2025-12-07
status: production
category: documentation
tags: [api-docs, openapi, swagger, rest-api, graphql, sdk, developer-experience]
tools: [Read, Write, Edit, Glob, Grep, WebSearch]
integrations: [technical-writer, code-review-assistant, tool-use-designer]
outputs: [openapi-specs, api-references, sdk-docs, integration-guides, postman-collections]
complexity: medium
---

# API Documentation Generator

## Purpose

Generate professional, comprehensive API documentation from source code, specifications, or descriptions. Create OpenAPI/Swagger specs, endpoint references, SDK documentation, and integration guides that provide excellent developer experience.

---

## Activation Triggers

Use this skill when the user:
- Asks to "document this API" or "generate API docs"
- Needs an "OpenAPI spec" or "Swagger file"
- Wants to "document endpoints"
- Needs "SDK documentation"
- Asks for "API reference" documentation
- Wants to generate "Postman collection"
- Needs "GraphQL schema documentation"

---

## Documentation Types

### 1. OpenAPI Specification
- Complete OpenAPI 3.0/3.1 YAML/JSON specs
- Schemas, endpoints, authentication
- Machine-readable format

### 2. API Reference
- Human-readable endpoint documentation
- Request/response examples
- Error code references

### 3. SDK Documentation
- Client library usage guides
- Language-specific examples
- Installation and setup

### 4. Integration Guides
- Step-by-step integration tutorials
- Authentication setup
- Common use cases

---

## Execution Workflow

### Phase 1: Source Analysis

**Step 1.1: Identify API Type**

| API Type | Indicators | Output Format |
|----------|------------|---------------|
| REST | HTTP methods, URL paths | OpenAPI 3.x |
| GraphQL | Queries, mutations, types | GraphQL SDL + docs |
| gRPC | Protobuf definitions | Proto docs |
| WebSocket | Event-based, bidirectional | Event catalog |

**Step 1.2: Gather API Information**

```
Extract from code/spec:
- Base URL and versioning
- Authentication methods
- Endpoints/operations
- Request/response schemas
- Error codes
- Rate limits
- Pagination patterns
```

**Step 1.3: Identify Documentation Scope**

```
□ Full API specification (OpenAPI)
□ Endpoint reference only
□ Single endpoint documentation
□ SDK/client library docs
□ Integration guide
□ All of the above
```

---

### Phase 2: OpenAPI Specification Generation

**Step 2.1: Basic OpenAPI Structure**

```yaml
openapi: 3.1.0
info:
  title: API Name
  description: |
    Brief description of what this API does.

    ## Authentication
    This API uses Bearer token authentication.

    ## Rate Limiting
    100 requests per minute per API key.
  version: 1.0.0
  contact:
    name: API Support
    email: api@example.com
    url: https://example.com/support
  license:
    name: MIT
    url: https://opensource.org/licenses/MIT

servers:
  - url: https://api.example.com/v1
    description: Production server
  - url: https://staging-api.example.com/v1
    description: Staging server

tags:
  - name: Users
    description: User management operations
  - name: Products
    description: Product catalog operations

paths:
  # Endpoints defined here

components:
  # Schemas, security schemes, etc.
```

**Step 2.2: Endpoint Documentation**

```yaml
paths:
  /users:
    get:
      operationId: listUsers
      summary: List all users
      description: |
        Retrieves a paginated list of users. Results can be filtered
        by status and sorted by creation date.
      tags:
        - Users
      parameters:
        - name: status
          in: query
          description: Filter by user status
          required: false
          schema:
            type: string
            enum: [active, inactive, pending]
        - name: limit
          in: query
          description: Maximum number of results (1-100)
          required: false
          schema:
            type: integer
            minimum: 1
            maximum: 100
            default: 20
        - name: offset
          in: query
          description: Number of results to skip
          required: false
          schema:
            type: integer
            minimum: 0
            default: 0
      responses:
        '200':
          description: Successful response
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/UserList'
              example:
                data:
                  - id: "usr_abc123"
                    email: "john@example.com"
                    name: "John Doe"
                    status: "active"
                total: 150
                limit: 20
                offset: 0
        '401':
          $ref: '#/components/responses/Unauthorized'
        '429':
          $ref: '#/components/responses/RateLimited'
      security:
        - bearerAuth: []

    post:
      operationId: createUser
      summary: Create a new user
      description: Creates a new user account with the provided information.
      tags:
        - Users
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/CreateUserRequest'
            example:
              email: "john@example.com"
              name: "John Doe"
              role: "member"
      responses:
        '201':
          description: User created successfully
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/User'
        '400':
          $ref: '#/components/responses/ValidationError'
        '409':
          description: Email already exists
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Error'
              example:
                code: "EMAIL_EXISTS"
                message: "A user with this email already exists"
      security:
        - bearerAuth: []

  /users/{userId}:
    get:
      operationId: getUser
      summary: Get user by ID
      description: Retrieves a specific user by their unique identifier.
      tags:
        - Users
      parameters:
        - name: userId
          in: path
          required: true
          description: Unique user identifier
          schema:
            type: string
            pattern: '^usr_[a-zA-Z0-9]+$'
          example: "usr_abc123"
      responses:
        '200':
          description: Successful response
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/User'
        '404':
          $ref: '#/components/responses/NotFound'
      security:
        - bearerAuth: []
```

**Step 2.3: Schema Definitions**

```yaml
components:
  schemas:
    User:
      type: object
      description: A user account
      required:
        - id
        - email
        - name
        - status
        - createdAt
      properties:
        id:
          type: string
          description: Unique identifier
          pattern: '^usr_[a-zA-Z0-9]+$'
          example: "usr_abc123"
        email:
          type: string
          format: email
          description: User's email address
          example: "john@example.com"
        name:
          type: string
          description: User's display name
          minLength: 1
          maxLength: 100
          example: "John Doe"
        status:
          type: string
          enum: [active, inactive, pending]
          description: Account status
          example: "active"
        role:
          type: string
          enum: [admin, member, guest]
          description: User's role
          default: "member"
        createdAt:
          type: string
          format: date-time
          description: Account creation timestamp
          example: "2024-01-15T10:30:00Z"
        updatedAt:
          type: string
          format: date-time
          description: Last update timestamp

    CreateUserRequest:
      type: object
      required:
        - email
        - name
      properties:
        email:
          type: string
          format: email
          description: User's email address
        name:
          type: string
          description: User's display name
          minLength: 1
          maxLength: 100
        role:
          type: string
          enum: [admin, member, guest]
          default: "member"

    UserList:
      type: object
      properties:
        data:
          type: array
          items:
            $ref: '#/components/schemas/User'
        total:
          type: integer
          description: Total number of users
        limit:
          type: integer
          description: Number of results returned
        offset:
          type: integer
          description: Number of results skipped

    Error:
      type: object
      required:
        - code
        - message
      properties:
        code:
          type: string
          description: Error code
          example: "VALIDATION_ERROR"
        message:
          type: string
          description: Human-readable error message
          example: "Invalid input provided"
        details:
          type: array
          items:
            type: object
            properties:
              field:
                type: string
              message:
                type: string
```

**Step 2.4: Authentication & Security**

```yaml
components:
  securitySchemes:
    bearerAuth:
      type: http
      scheme: bearer
      bearerFormat: JWT
      description: |
        JWT token obtained from /auth/login endpoint.

        Example: `Authorization: Bearer eyJhbGciOiJIUzI1NiIs...`

    apiKey:
      type: apiKey
      in: header
      name: X-API-Key
      description: API key for server-to-server authentication

    oauth2:
      type: oauth2
      description: OAuth 2.0 authentication
      flows:
        authorizationCode:
          authorizationUrl: https://auth.example.com/authorize
          tokenUrl: https://auth.example.com/token
          scopes:
            read:users: Read user data
            write:users: Create and update users
            admin: Full administrative access

# Default security for all endpoints
security:
  - bearerAuth: []
```

**Step 2.5: Reusable Responses**

```yaml
components:
  responses:
    Unauthorized:
      description: Authentication required
      content:
        application/json:
          schema:
            $ref: '#/components/schemas/Error'
          example:
            code: "UNAUTHORIZED"
            message: "Authentication required"

    Forbidden:
      description: Insufficient permissions
      content:
        application/json:
          schema:
            $ref: '#/components/schemas/Error'
          example:
            code: "FORBIDDEN"
            message: "You don't have permission to perform this action"

    NotFound:
      description: Resource not found
      content:
        application/json:
          schema:
            $ref: '#/components/schemas/Error'
          example:
            code: "NOT_FOUND"
            message: "The requested resource was not found"

    ValidationError:
      description: Invalid request data
      content:
        application/json:
          schema:
            $ref: '#/components/schemas/Error'
          example:
            code: "VALIDATION_ERROR"
            message: "Invalid input"
            details:
              - field: "email"
                message: "Must be a valid email address"

    RateLimited:
      description: Rate limit exceeded
      headers:
        X-RateLimit-Limit:
          schema:
            type: integer
          description: Request limit per minute
        X-RateLimit-Remaining:
          schema:
            type: integer
          description: Remaining requests
        X-RateLimit-Reset:
          schema:
            type: integer
          description: Unix timestamp when limit resets
      content:
        application/json:
          schema:
            $ref: '#/components/schemas/Error'
          example:
            code: "RATE_LIMITED"
            message: "Too many requests. Try again in 60 seconds."
```

---

### Phase 3: Human-Readable API Reference

**Markdown API Reference Template:**

```markdown
# API Reference

## Base URL

```
https://api.example.com/v1
```

## Authentication

All API requests require authentication using a Bearer token:

```bash
curl -H "Authorization: Bearer YOUR_TOKEN" \
  https://api.example.com/v1/users
```

Obtain a token by calling the `/auth/login` endpoint.

---

## Users

### List Users

Retrieves a paginated list of users.

**Endpoint:** `GET /users`

**Query Parameters:**

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| status | string | No | Filter: `active`, `inactive`, `pending` |
| limit | integer | No | Results per page (1-100). Default: 20 |
| offset | integer | No | Skip N results. Default: 0 |

**Request:**

```bash
curl -X GET "https://api.example.com/v1/users?status=active&limit=10" \
  -H "Authorization: Bearer YOUR_TOKEN"
```

**Response (200):**

```json
{
  "data": [
    {
      "id": "usr_abc123",
      "email": "john@example.com",
      "name": "John Doe",
      "status": "active",
      "createdAt": "2024-01-15T10:30:00Z"
    }
  ],
  "total": 150,
  "limit": 10,
  "offset": 0
}
```

---

### Create User

Creates a new user account.

**Endpoint:** `POST /users`

**Request Body:**

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| email | string | Yes | Valid email address |
| name | string | Yes | Display name (1-100 chars) |
| role | string | No | `admin`, `member`, `guest`. Default: `member` |

**Request:**

```bash
curl -X POST "https://api.example.com/v1/users" \
  -H "Authorization: Bearer YOUR_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "email": "john@example.com",
    "name": "John Doe",
    "role": "member"
  }'
```

**Response (201):**

```json
{
  "id": "usr_abc123",
  "email": "john@example.com",
  "name": "John Doe",
  "status": "active",
  "role": "member",
  "createdAt": "2024-01-15T10:30:00Z"
}
```

**Errors:**

| Status | Code | Description |
|--------|------|-------------|
| 400 | VALIDATION_ERROR | Invalid request body |
| 409 | EMAIL_EXISTS | Email already registered |

---

## Error Codes

All errors return a JSON object with `code` and `message`:

```json
{
  "code": "ERROR_CODE",
  "message": "Human-readable description"
}
```

| Code | HTTP Status | Description |
|------|-------------|-------------|
| UNAUTHORIZED | 401 | Missing or invalid auth token |
| FORBIDDEN | 403 | Insufficient permissions |
| NOT_FOUND | 404 | Resource doesn't exist |
| VALIDATION_ERROR | 400 | Invalid input data |
| EMAIL_EXISTS | 409 | Email already in use |
| RATE_LIMITED | 429 | Too many requests |
| SERVER_ERROR | 500 | Internal server error |

---

## Rate Limiting

- **Limit:** 100 requests per minute
- **Headers:** Check `X-RateLimit-Remaining` for current quota

When rate limited, wait until `X-RateLimit-Reset` timestamp.
```

---

### Phase 4: SDK Documentation

**JavaScript/TypeScript SDK Example:**

```markdown
# JavaScript SDK

## Installation

```bash
npm install @company/api-sdk
# or
yarn add @company/api-sdk
```

## Quick Start

```typescript
import { Client } from '@company/api-sdk';

const client = new Client({
  apiKey: 'your-api-key',
  // Optional: custom base URL
  baseUrl: 'https://api.example.com/v1'
});

// List users
const users = await client.users.list({ limit: 10 });
console.log(users.data);

// Create user
const newUser = await client.users.create({
  email: 'john@example.com',
  name: 'John Doe'
});
console.log(newUser.id);
```

## Configuration Options

| Option | Type | Required | Description |
|--------|------|----------|-------------|
| apiKey | string | Yes | Your API key |
| baseUrl | string | No | API base URL |
| timeout | number | No | Request timeout (ms). Default: 30000 |
| retries | number | No | Retry attempts. Default: 3 |

## Users

### List Users

```typescript
const response = await client.users.list({
  status: 'active',  // optional
  limit: 20,         // optional, default: 20
  offset: 0          // optional, default: 0
});

// response.data: User[]
// response.total: number
// response.limit: number
// response.offset: number
```

### Get User

```typescript
const user = await client.users.get('usr_abc123');
// Returns: User object
```

### Create User

```typescript
const user = await client.users.create({
  email: 'john@example.com',
  name: 'John Doe',
  role: 'member'  // optional
});
// Returns: User object with id
```

### Update User

```typescript
const user = await client.users.update('usr_abc123', {
  name: 'John Updated'
});
```

### Delete User

```typescript
await client.users.delete('usr_abc123');
// Returns: void
```

## Error Handling

```typescript
import { ApiError, ValidationError, NotFoundError } from '@company/api-sdk';

try {
  const user = await client.users.get('invalid-id');
} catch (error) {
  if (error instanceof NotFoundError) {
    console.log('User not found');
  } else if (error instanceof ValidationError) {
    console.log('Invalid input:', error.details);
  } else if (error instanceof ApiError) {
    console.log('API error:', error.code, error.message);
  }
}
```

## TypeScript Types

```typescript
import type { User, CreateUserInput, UserListResponse } from '@company/api-sdk';

const input: CreateUserInput = {
  email: 'john@example.com',
  name: 'John Doe'
};

const user: User = await client.users.create(input);
```
```

---

### Phase 5: Output Formats

**OpenAPI Spec (YAML):**
- Complete machine-readable specification
- Suitable for Swagger UI, code generation

**OpenAPI Spec (JSON):**
- Alternative format for tooling
- Same content as YAML

**Markdown Reference:**
- Human-readable documentation
- Suitable for README, docs sites

**Postman Collection:**
- Importable to Postman
- Pre-configured requests

---

## Quality Checklist

### OpenAPI Spec
- [ ] Valid OpenAPI 3.0+ syntax
- [ ] All endpoints documented
- [ ] Request/response schemas defined
- [ ] Examples provided
- [ ] Authentication documented
- [ ] Error responses included

### API Reference
- [ ] Clear endpoint descriptions
- [ ] Parameter tables complete
- [ ] Code examples work
- [ ] Error codes explained
- [ ] Authentication covered

### SDK Docs
- [ ] Installation instructions
- [ ] Quick start example
- [ ] All methods documented
- [ ] TypeScript types shown
- [ ] Error handling examples

---

## Integration with Other Skills

### With technical-writer:
- Generate integration guides
- Create getting started tutorials

### With tool-use-designer:
- Document Claude tool APIs
- Create tool schema references

### With code-review-assistant:
- Review API design patterns
- Check for security issues

---

## Troubleshooting

### OpenAPI validation fails
- Check YAML/JSON syntax
- Validate with online tools
- Ensure $ref paths are correct

### Examples don't match schemas
- Regenerate examples from schemas
- Check required fields

### Missing endpoints
- Review source code thoroughly
- Check for dynamic routes

---

## Version History

- v1.0.0 (2025-12-07): Initial release with OpenAPI generation, markdown references, and SDK documentation patterns
