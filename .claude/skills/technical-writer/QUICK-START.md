# Technical Writer - Quick Start

## Request Documentation

```
Document [code/API/feature].
Audience: [who will read this]
Format: [README/API docs/guide]
```

---

## README Template

```markdown
# Project Name

> One-line description

## Install

```bash
npm install project
```

## Usage

```javascript
// minimal working example
```

## Configuration

| Option | Default | Description |
|--------|---------|-------------|
| key | value | what it does |

## License

MIT
```

---

## API Endpoint Template

```markdown
### POST /endpoint

Description of what it does.

**Request:**
```json
{ "field": "value" }
```

**Response (200):**
```json
{ "id": "123", "field": "value" }
```

**Errors:**
| Code | Description |
|------|-------------|
| 400 | Bad request |
| 401 | Unauthorized |
```

---

## Function Documentation

```markdown
### functionName(param1, param2)

What it does.

**Parameters:**
- `param1` (string): Description
- `param2` (number?): Optional. Default: 10

**Returns:** Description

**Example:**
```javascript
const result = functionName('value');
```
```

---

## Writing Checklist

- [ ] Active voice ("Run the command" not "The command should be run")
- [ ] Second person ("you" not "one")
- [ ] Present tense ("returns" not "will return")
- [ ] Complete, working code examples
- [ ] No unexplained jargon

---

## Quick Fixes

| Problem | Fix |
|---------|-----|
| Too long | Break into files, add TOC |
| Can't find info | Improve headings/structure |
| Examples broken | Test all code |
| Inconsistent terms | Create glossary |

---

## Common Structures

**Tutorial:** Prerequisites → Steps → Verification → Next Steps

**Reference:** Overview → Parameters → Returns → Examples → Errors

**Guide:** Goal → Prerequisites → Steps → Troubleshooting → Support
