---
name: Technical Writer
description: Professional technical documentation specialist that creates clear, comprehensive documentation including API references, user guides, READMEs, integration guides, and developer tutorials
version: 1.0.0
author: 360 Social Impact Studios
created: 2025-12-07
updated: 2025-12-07
status: production
category: documentation
tags: [documentation, api-docs, readme, user-guides, technical-writing, developer-experience]
tools: [Read, Write, Edit, Glob, Grep, WebSearch]
integrations: [prompt-engineer, code-review-assistant, tool-use-designer]
outputs: [api-documentation, readme-files, user-guides, integration-guides, tutorials, changelogs]
complexity: medium
---

# Technical Writer

## Purpose

Create professional, clear, and comprehensive technical documentation. Transform code, specifications, and technical knowledge into accessible documentation that serves developers, users, and stakeholders effectively.

---

## Activation Triggers

Use this skill when the user:
- Asks to "document this code" or "write documentation"
- Needs an "API reference" or "API docs"
- Wants to "create a README" for their project
- Needs a "user guide" or "getting started" guide
- Asks for "integration documentation"
- Wants a "changelog" or "release notes"
- Needs "developer tutorials" or "how-to guides"

---

## Documentation Types

### 1. API Documentation
- Endpoint references
- Request/response schemas
- Authentication guides
- Error code references
- Rate limiting information

### 2. README Files
- Project overview
- Installation instructions
- Quick start guide
- Configuration options
- Contributing guidelines

### 3. User Guides
- Getting started tutorials
- Feature documentation
- Troubleshooting guides
- FAQ sections

### 4. Integration Guides
- Setup instructions
- Configuration details
- Code examples
- Best practices

### 5. Developer References
- Architecture overviews
- Code conventions
- API client libraries
- SDK documentation

---

## Execution Workflow

### Phase 1: Requirements Gathering

**Step 1.1: Understand the Documentation Need**

```
Gather from user:
- What needs to be documented?
- Who is the target audience?
- What format is preferred?
- Are there existing docs to extend?
- What's the technical level of readers?
- Any style guide to follow?
```

**Step 1.2: Assess Source Material**

```
Review available:
□ Source code
□ Existing documentation
□ API specifications (OpenAPI, etc.)
□ Architecture diagrams
□ Team knowledge
□ User feedback/questions
```

**Step 1.3: Define Documentation Scope**

| Scope Level | Description |
|-------------|-------------|
| **Reference** | Comprehensive API/function reference |
| **Guide** | Task-oriented how-to documentation |
| **Tutorial** | Learning-oriented step-by-step |
| **Explanation** | Understanding-oriented background |

---

### Phase 2: Documentation Patterns

#### Pattern A: API Reference Documentation

**Structure:**
```markdown
# API Reference

## Overview
[Brief description of the API]

## Base URL
`https://api.example.com/v1`

## Authentication
[Auth method and examples]

## Endpoints

### [Resource Name]

#### GET /resource
[Description]

**Parameters:**
| Name | Type | Required | Description |
|------|------|----------|-------------|
| id | string | Yes | Resource ID |

**Request Example:**
```bash
curl -X GET "https://api.example.com/v1/resource/123" \
  -H "Authorization: Bearer TOKEN"
```

**Response:**
```json
{
  "id": "123",
  "name": "Example"
}
```

**Error Codes:**
| Code | Description |
|------|-------------|
| 400 | Bad request |
| 404 | Not found |

---
```

**OpenAPI-Style Endpoint Documentation:**

```markdown
### Create User

Creates a new user account.

**Endpoint:** `POST /users`

**Request Body:**
```json
{
  "email": "user@example.com",
  "name": "John Doe",
  "role": "member"
}
```

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| email | string | Yes | Valid email address |
| name | string | Yes | Display name (2-100 chars) |
| role | string | No | User role. Default: "member" |

**Success Response (201):**
```json
{
  "id": "usr_abc123",
  "email": "user@example.com",
  "name": "John Doe",
  "role": "member",
  "created_at": "2024-01-15T10:30:00Z"
}
```

**Error Responses:**

| Status | Code | Description |
|--------|------|-------------|
| 400 | VALIDATION_ERROR | Invalid request body |
| 409 | EMAIL_EXISTS | Email already registered |
| 429 | RATE_LIMITED | Too many requests |
```

---

#### Pattern B: README Documentation

**Standard README Structure:**

```markdown
# Project Name

> One-line description of what this project does

[![Build Status](badge)](link)
[![License](badge)](link)

## Features

- Feature 1 with brief explanation
- Feature 2 with brief explanation
- Feature 3 with brief explanation

## Installation

### Prerequisites

- Requirement 1 (version)
- Requirement 2 (version)

### Quick Install

```bash
npm install project-name
```

### Manual Installation

```bash
git clone https://github.com/org/project
cd project
npm install
```

## Quick Start

```javascript
import { Client } from 'project-name';

const client = new Client({ apiKey: 'your-key' });
const result = await client.doSomething();
```

## Configuration

| Option | Type | Default | Description |
|--------|------|---------|-------------|
| apiKey | string | - | Your API key |
| timeout | number | 5000 | Request timeout (ms) |
| retries | number | 3 | Retry attempts |

## Usage Examples

### Basic Usage
[Code example with explanation]

### Advanced Usage
[Code example with explanation]

## API Reference

See [API Documentation](./docs/api.md) for complete reference.

## Contributing

See [CONTRIBUTING.md](./CONTRIBUTING.md) for guidelines.

## License

MIT - see [LICENSE](./LICENSE)
```

---

#### Pattern C: User Guide Documentation

**Getting Started Guide:**

```markdown
# Getting Started with [Product]

This guide walks you through setting up [Product] and completing your first [task].

## Prerequisites

Before you begin, ensure you have:
- [ ] Requirement 1
- [ ] Requirement 2
- [ ] Account access (sign up at [link])

## Step 1: Installation

[Clear step with code/screenshots]

## Step 2: Configuration

[Clear step with code/screenshots]

## Step 3: Your First [Task]

[Clear step with expected outcome]

## What's Next?

Now that you've [completed task], you can:
- [Next task with link]
- [Another option with link]
- [Advanced topic with link]

## Troubleshooting

### Common Issues

**Issue:** [Problem description]
**Solution:** [Fix steps]

**Issue:** [Problem description]
**Solution:** [Fix steps]

## Getting Help

- [Documentation link]
- [Community forum link]
- [Support contact]
```

---

#### Pattern D: Integration Guide

```markdown
# [Service] Integration Guide

Integrate [Product] with [Service] to [benefit].

## Overview

This integration enables:
- Capability 1
- Capability 2
- Capability 3

**Time to complete:** ~15 minutes

## Prerequisites

- [Product] account with [plan] access
- [Service] account with admin permissions
- API key from [Product] dashboard

## Step 1: Configure [Service]

1. Navigate to Settings > Integrations
2. Click "Add Integration"
3. Select "[Product]"

## Step 2: Connect [Product]

1. In [Product] dashboard, go to Integrations
2. Enter your [Service] credentials:
   - API Key: [from Step 1]
   - Webhook URL: [from Step 1]
3. Click "Test Connection"

## Step 3: Configure Data Sync

Select which data to sync:

| Data Type | Direction | Frequency |
|-----------|-----------|-----------|
| Users | [Service] → [Product] | Real-time |
| Events | [Product] → [Service] | 5 minutes |

## Verification

To verify the integration is working:

1. [Action to test]
2. Check [location] for [expected result]
3. Confirm [final verification]

## Advanced Configuration

### Custom Field Mapping

```json
{
  "field_mappings": {
    "service_field": "product_field"
  }
}
```

### Webhook Events

Available webhook events:
- `user.created` - New user registration
- `order.completed` - Order finalized

## Troubleshooting

| Symptom | Cause | Solution |
|---------|-------|----------|
| Sync not running | Invalid credentials | Regenerate API key |
| Data missing | Field mapping | Check mapping config |

## Support

For integration support:
- Email: integrations@product.com
- Docs: docs.product.com/integrations/service
```

---

#### Pattern E: Changelog/Release Notes

```markdown
# Changelog

All notable changes to this project are documented here.

Format based on [Keep a Changelog](https://keepachangelog.com/).

## [Unreleased]

### Added
- Feature in development

## [2.1.0] - 2024-01-15

### Added
- New `search` endpoint with full-text support (#123)
- Rate limiting headers in all responses
- Support for bulk operations

### Changed
- Improved error messages for validation failures
- Updated Node.js requirement to v18+

### Fixed
- Memory leak in connection pooling (#456)
- Incorrect timestamp format in webhooks

### Security
- Updated dependencies to patch CVE-2024-xxxx

### Deprecated
- `v1/legacy` endpoints (removal in v3.0)

## [2.0.0] - 2024-01-01

### Breaking Changes
- Renamed `userId` to `user_id` in all endpoints
- Removed deprecated `v1/old-endpoint`

### Migration Guide
See [MIGRATION.md](./MIGRATION.md) for upgrade instructions.
```

---

### Phase 3: Writing Guidelines

**Step 3.1: Voice and Tone**

| Aspect | Guideline |
|--------|-----------|
| **Voice** | Active, direct, professional |
| **Tone** | Helpful, confident, approachable |
| **Person** | Second person ("you") for instructions |
| **Tense** | Present tense for current behavior |

**Examples:**

```
GOOD: "Run the command to install dependencies."
BAD: "The command should be run to install dependencies."

GOOD: "This method returns an array of users."
BAD: "This method will return an array of users."

GOOD: "You can configure the timeout using the settings file."
BAD: "One can configure the timeout using the settings file."
```

**Step 3.2: Code Examples**

Every code example should:
- Be complete enough to copy-paste
- Include necessary imports
- Use realistic (not foo/bar) values
- Show expected output when relevant
- Be tested/verified to work

```javascript
// GOOD: Complete, realistic example
import { Client } from '@product/sdk';

const client = new Client({
  apiKey: process.env.PRODUCT_API_KEY,
  region: 'us-east-1'
});

const users = await client.users.list({ limit: 10 });
console.log(`Found ${users.length} users`);

// BAD: Incomplete, unrealistic
import { Client } from '@product/sdk';
client.foo();
```

**Step 3.3: Formatting Standards**

```markdown
# Heading 1 (Page Title)
## Heading 2 (Major Sections)
### Heading 3 (Subsections)
#### Heading 4 (Minor Points)

**Bold** for emphasis and UI elements
`code` for inline code, commands, file names
```code``` for code blocks with language specified

- Bullet lists for unordered items
1. Numbered lists for sequential steps

| Tables | For | Structured Data |
|--------|-----|-----------------|

> Blockquotes for important notes or warnings

[Links](url) with descriptive text, not "click here"
```

**Step 3.4: Information Architecture**

```
Organize content by user goal, not by feature:

GOOD:
"How to deploy your application"
  → Prerequisites
  → Prepare your app
  → Configure deployment
  → Deploy
  → Verify

BAD:
"Deployment Service"
  → Overview
  → Features
  → API Reference
  → Configuration
```

---

### Phase 4: Quality Checklist

**Content Quality:**
- [ ] Accurate and up-to-date
- [ ] Complete (no missing steps)
- [ ] Consistent terminology
- [ ] Appropriate depth for audience
- [ ] Examples are tested and work

**Structure Quality:**
- [ ] Logical organization
- [ ] Easy to navigate
- [ ] Clear headings
- [ ] Scannable format
- [ ] Progressive disclosure (simple → complex)

**Writing Quality:**
- [ ] Clear and concise
- [ ] Active voice
- [ ] No jargon (or explained when used)
- [ ] Grammatically correct
- [ ] Accessible (no assumptions)

**Technical Quality:**
- [ ] Code examples work
- [ ] Commands are correct
- [ ] Links are valid
- [ ] Versions are specified
- [ ] Edge cases addressed

---

### Phase 5: Output Formats

**Markdown (Default):**
- Most common for developer docs
- GitHub/GitLab compatible
- Easy to version control

**HTML:**
- For hosted documentation
- Include styling recommendations

**OpenAPI/Swagger:**
- For API specifications
- Machine-readable format

---

## Documentation Templates

### Minimal README
```markdown
# Project Name

Brief description.

## Install

```bash
npm install project-name
```

## Usage

```javascript
// minimal example
```

## License

MIT
```

### Function/Method Documentation
```markdown
### functionName(param1, param2)

Brief description of what the function does.

**Parameters:**
- `param1` (string): Description of param1
- `param2` (number, optional): Description. Default: 10

**Returns:**
- (Promise<Result>): Description of return value

**Throws:**
- `ValidationError`: When input is invalid

**Example:**
```javascript
const result = await functionName('value', 20);
```
```

### CLI Command Documentation
```markdown
## command-name

Description of what the command does.

### Usage

```bash
command-name [options] <required-arg>
```

### Arguments

| Argument | Description |
|----------|-------------|
| required-arg | Description |

### Options

| Option | Default | Description |
|--------|---------|-------------|
| -f, --flag | false | Description |
| -o, --output | stdout | Description |

### Examples

```bash
# Basic usage
command-name input.txt

# With options
command-name -f -o output.txt input.txt
```
```

---

## Integration with Other Skills

### With prompt-engineer:
- Document prompt templates
- Create prompt engineering guides

### With code-review-assistant:
- Document code review standards
- Create contribution guidelines

### With tool-use-designer:
- Document tool schemas
- Create tool integration guides

---

## Troubleshooting

### Documentation too long
- Break into multiple files
- Add table of contents
- Use progressive disclosure

### Users can't find information
- Improve navigation/structure
- Add search functionality
- Cross-reference related topics

### Code examples don't work
- Test all examples
- Include version information
- Add troubleshooting section

### Inconsistent terminology
- Create glossary
- Use consistent naming
- Search and replace inconsistencies

---

## Version History

- v1.0.0 (2025-12-07): Initial release with API docs, README, user guides, integration guides, and changelog patterns
