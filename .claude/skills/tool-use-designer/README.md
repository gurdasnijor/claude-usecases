# Tool Use Designer

> Design effective Claude tool schemas and orchestration patterns for agentic applications

## Overview

The Tool Use Designer helps developers create well-structured tool definitions for Claude API applications. It covers schema design, naming conventions, error handling, and multi-tool orchestration patterns.

## When to Use

- **Designing new tools** for Claude-powered applications
- **Building agents** with multi-step workflows
- **Connecting Claude to APIs** and external systems
- **Debugging tool selection** issues
- **Optimizing tool schemas** for reliability

## Key Capabilities

| Capability | Description |
|------------|-------------|
| **Schema Design** | Create clear, effective tool definitions |
| **Naming Conventions** | Follow best practices for tool/parameter names |
| **Description Writing** | Write descriptions that guide tool selection |
| **Error Handling** | Design robust error response patterns |
| **Orchestration Patterns** | Build multi-tool workflows |

## Quick Example

### Input Request
```
I need a tool for Claude to search our product catalog
```

### Output Schema
```json
{
  "name": "search_products",
  "description": "Search the product catalog by keywords, category, or price range. Use this when the user wants to find products or compare options. Returns up to 10 matching products with name, price, and availability.",
  "input_schema": {
    "type": "object",
    "properties": {
      "query": {
        "type": "string",
        "description": "Search keywords"
      },
      "category": {
        "type": "string",
        "enum": ["electronics", "clothing", "home", "sports"],
        "description": "Product category filter"
      },
      "max_price": {
        "type": "number",
        "description": "Maximum price in USD"
      },
      "limit": {
        "type": "integer",
        "description": "Number of results (1-20). Default: 10",
        "minimum": 1,
        "maximum": 20
      }
    },
    "required": ["query"]
  }
}
```

## Orchestration Patterns

| Pattern | Use Case |
|---------|----------|
| **Sequential** | tool_a → tool_b → tool_c |
| **Conditional** | if result then tool_b else tool_c |
| **Parallel** | tool_a + tool_b simultaneously |
| **Iterative** | repeat until condition met |
| **Validation Chain** | validate → action → confirm |

## Tool Description Formula

```
[What it does] + [When to use it] + [What it returns]
```

Example:
```
"Retrieve user profile data including name, email, and preferences.
Use when user asks about their account information.
Returns user object with all profile fields."
```

## Common Issues & Fixes

| Issue | Solution |
|-------|----------|
| Wrong tool selected | Make descriptions more distinct |
| Parameters hallucinated | Add descriptions, reduce required fields |
| Workflow breaks | Simplify, add intermediate confirmations |
| Errors not handled | Implement clear error response format |

## Related Skills

- **prompt-engineer** - Optimize system prompts for tool-using agents
- **code-review-assistant** - Review tool implementation code

## Version

- **Current:** v1.0.0
- **Last Updated:** 2025-12-07
- **Author:** 360 Social Impact Studios
