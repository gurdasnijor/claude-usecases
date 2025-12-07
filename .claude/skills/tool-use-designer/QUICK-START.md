# Tool Use Designer - Quick Start

## Schema Template

```json
{
  "name": "action_resource",
  "description": "[What] + [When to use] + [Returns]",
  "input_schema": {
    "type": "object",
    "properties": {
      "param": {
        "type": "string",
        "description": "Clear description"
      }
    },
    "required": ["param"]
  }
}
```

---

## Naming Conventions

| DO | DON'T |
|----|-------|
| `get_user_profile` | `getUserProfile` |
| `search_products` | `search` |
| `send_email` | `email_tool` |
| `create_order` | `do_thing` |

---

## Description Formula

```
[What it does] + [When to use it] + [What it returns]
```

Example:
```
"Search products by keywords or category.
Use when user wants to find or compare products.
Returns up to 10 matching items with name, price, availability."
```

---

## Parameter Types

| Type | Use For |
|------|---------|
| `string` | Text, IDs, enums |
| `number` | Decimals, prices |
| `integer` | Counts, limits |
| `boolean` | Flags, toggles |
| `array` | Lists of items |
| `object` | Nested data |

---

## Useful Constraints

```json
{
  "status": {
    "type": "string",
    "enum": ["pending", "active", "done"]
  },
  "limit": {
    "type": "integer",
    "minimum": 1,
    "maximum": 100
  },
  "email": {
    "type": "string",
    "description": "Valid email address"
  }
}
```

---

## Error Response Format

```json
{
  "success": false,
  "error": {
    "code": "NOT_FOUND",
    "message": "User not found",
    "suggestion": "Check user ID"
  }
}
```

---

## Orchestration Patterns

**Sequential:**
```
search → get_details → add_to_cart
```

**Conditional:**
```
check_stock → (yes) reserve | (no) notify
```

**Parallel:**
```
[get_price_a, get_price_b, get_price_c] → compare
```

---

## Checklist

- [ ] Descriptive snake_case name
- [ ] Description: what + when + returns
- [ ] All params have descriptions
- [ ] Required fields marked
- [ ] Formats specified (dates, IDs)
- [ ] Enums for fixed options
- [ ] Error handling defined

---

## Common Fixes

| Problem | Solution |
|---------|----------|
| Wrong tool picked | Add "Use when..." to description |
| Missing params | Add defaults, reduce required |
| Hallucinated values | Add format examples |
| Workflows break | Add confirmation steps |
