---
name: Tool Use Designer
description: Expert designer for Claude tool schemas, orchestration patterns, and agentic workflows. Helps developers create effective tool definitions, handle tool results, and build reliable Claude-powered applications
version: 1.0.0
author: 360 Social Impact Studios
created: 2025-12-07
updated: 2025-12-07
status: production
category: claude-api-optimization
tags: [tools, function-calling, agents, orchestration, schemas, claude-api, automation]
tools: [Read, Write, Edit, WebSearch]
integrations: [prompt-engineer, code-review-assistant]
outputs: [tool-schemas, orchestration-patterns, implementation-guides, error-handling]
complexity: medium
---

# Tool Use Designer

## Purpose

Design effective tool schemas for Claude API applications. Create clear, well-structured tool definitions that enable Claude to reliably select and use tools. Build orchestration patterns for multi-tool workflows and agentic systems.

---

## Activation Triggers

Use this skill when the user:
- Needs to "create a tool" or "define tools" for Claude
- Is building an "agent" or "agentic workflow"
- Asks about "function calling" with Claude
- Wants to "connect Claude to external APIs"
- Needs help with tool result handling
- Is debugging tool selection issues
- Asks about multi-step tool orchestration

---

## Core Concepts

### What Are Claude Tools?

Tools enable Claude to interact with external systems by:
1. **Understanding** what tools are available (via schemas)
2. **Deciding** when a tool is needed
3. **Generating** structured tool calls
4. **Processing** tool results to continue the conversation

### Tool Schema Structure

```json
{
  "name": "tool_name",
  "description": "Clear description of what this tool does and when to use it",
  "input_schema": {
    "type": "object",
    "properties": {
      "param1": {
        "type": "string",
        "description": "What this parameter is for"
      }
    },
    "required": ["param1"]
  }
}
```

---

## Execution Workflow

### Phase 1: Requirements Gathering

**Step 1.1: Understand the Use Case**
```
Gather from user:
- What external actions should Claude be able to take?
- What data sources should Claude access?
- What's the expected workflow/conversation pattern?
- Are there multi-step processes involved?
- What error conditions might occur?
```

**Step 1.2: Identify Tool Candidates**

| User Need | Tool Type |
|-----------|-----------|
| Read data from database | Data retrieval tool |
| Call external API | API wrapper tool |
| Perform calculations | Computation tool |
| Send notifications | Action tool |
| Search/query | Search tool |
| File operations | CRUD tool |
| Execute code | Execution tool |

---

### Phase 2: Schema Design

**Step 2.1: Naming Conventions**

```
DO:
- Use snake_case for tool names
- Use descriptive, action-oriented names
- Include the resource type when helpful

Examples:
✓ get_user_profile
✓ search_products
✓ send_email
✓ calculate_shipping_cost
✓ create_calendar_event

DON'T:
✗ getUserProfile (camelCase)
✗ user (too vague)
✗ do_thing (unclear action)
✗ tool1, tool2 (meaningless)
```

**Step 2.2: Description Best Practices**

The description is critical for tool selection. Include:

```json
{
  "name": "search_products",
  "description": "Search the product catalog by keywords, category, or price range. Use this when the user wants to find products or compare options. Returns up to 10 matching products with name, price, and availability."
}
```

**Description Formula:**
```
[What it does] + [When to use it] + [What it returns/affects]
```

**Good Descriptions:**
```
✓ "Get the current weather for a specific city. Use when user asks about weather conditions. Returns temperature, conditions, and humidity."

✓ "Send an email to specified recipients. Use when user explicitly requests to send an email. Requires recipient, subject, and body. Returns send confirmation."

✓ "Search company knowledge base for relevant documents. Use when user asks questions that require internal documentation. Returns top 5 matching document excerpts."
```

**Poor Descriptions:**
```
✗ "Gets weather" (too vague, no usage guidance)
✗ "This tool is used for..." (redundant phrasing)
✗ "Email tool" (no action, no guidance)
```

**Step 2.3: Parameter Design**

```json
{
  "input_schema": {
    "type": "object",
    "properties": {
      "user_id": {
        "type": "string",
        "description": "Unique identifier for the user (UUID format)"
      },
      "include_history": {
        "type": "boolean",
        "description": "Whether to include order history. Default: false"
      },
      "date_range": {
        "type": "object",
        "description": "Filter results by date range",
        "properties": {
          "start": {
            "type": "string",
            "description": "Start date in ISO 8601 format (YYYY-MM-DD)"
          },
          "end": {
            "type": "string",
            "description": "End date in ISO 8601 format (YYYY-MM-DD)"
          }
        }
      }
    },
    "required": ["user_id"]
  }
}
```

**Parameter Guidelines:**

| Guideline | Example |
|-----------|---------|
| Specify formats | "ISO 8601 format (YYYY-MM-DD)" |
| Indicate defaults | "Default: false" |
| Use enums for fixed options | `"enum": ["asc", "desc"]` |
| Constrain values | `"minimum": 1, "maximum": 100` |
| Mark required clearly | Include in `required` array |

**Step 2.4: Complex Parameter Patterns**

**Enum for Fixed Options:**
```json
{
  "status": {
    "type": "string",
    "enum": ["pending", "active", "completed", "cancelled"],
    "description": "Filter by order status"
  }
}
```

**Array Parameters:**
```json
{
  "tags": {
    "type": "array",
    "items": {
      "type": "string"
    },
    "description": "List of tags to filter by"
  }
}
```

**Nested Objects:**
```json
{
  "address": {
    "type": "object",
    "properties": {
      "street": { "type": "string" },
      "city": { "type": "string" },
      "country": { "type": "string" }
    },
    "required": ["city", "country"]
  }
}
```

---

### Phase 3: Tool Set Design

**Step 3.1: Tool Grouping Strategies**

**Option A: Fine-Grained Tools**
```
get_user
update_user
delete_user
list_users
```
- More explicit selection
- Claude can combine tools
- Clearer intent per call

**Option B: Combined CRUD Tool**
```
manage_user (with action parameter)
```
- Fewer tools to maintain
- Works well for simple CRUD
- May be less clear for Claude

**Recommendation:** Start fine-grained, combine if Claude struggles with selection.

**Step 3.2: Tool Relationships**

```
Define tool workflows:

1. Sequential: tool_a → tool_b → tool_c
   Example: search_products → get_product_details → add_to_cart

2. Conditional: if tool_a result, then tool_b else tool_c
   Example: check_inventory → (in stock) reserve_item OR (out of stock) notify_restock

3. Parallel: tool_a + tool_b simultaneously
   Example: get_weather + get_traffic (for trip planning)

4. Iterative: repeat tool_a until condition
   Example: paginated search until no more results
```

---

### Phase 4: Error Handling Design

**Step 4.1: Define Error Response Format**

```json
{
  "success": false,
  "error": {
    "code": "RATE_LIMIT_EXCEEDED",
    "message": "API rate limit exceeded. Try again in 60 seconds.",
    "retry_after": 60
  }
}
```

**Step 4.2: Common Error Types**

| Error Type | When | How Claude Should Respond |
|------------|------|---------------------------|
| `NOT_FOUND` | Resource doesn't exist | Inform user, suggest alternatives |
| `UNAUTHORIZED` | Permission denied | Explain limitation, suggest workaround |
| `VALIDATION_ERROR` | Invalid input | Fix input and retry |
| `RATE_LIMIT` | Too many requests | Wait and retry |
| `SERVICE_ERROR` | External failure | Apologize, suggest retry later |
| `TIMEOUT` | Request took too long | Inform user, offer to retry |

**Step 4.3: Graceful Degradation**

Design tools to return partial results when possible:

```json
{
  "success": true,
  "partial": true,
  "data": {
    "products": [...],
    "total": 150,
    "returned": 10
  },
  "message": "Returned first 10 of 150 results. Use pagination for more."
}
```

---

### Phase 5: Orchestration Patterns

**Pattern 1: Simple Request-Response**
```
User: "What's the weather in Paris?"
Claude: [thinks: need weather tool]
       → calls get_weather(city="Paris")
       ← receives {temp: 18, conditions: "sunny"}
       "It's currently 18°C and sunny in Paris."
```

**Pattern 2: Multi-Step with Context**
```
User: "Book me a flight to Tokyo next week"
Claude: [thinks: need multiple tools]
       → calls search_flights(destination="Tokyo", dates="next week")
       ← receives [flight options]
       "I found 5 options. [presents options]"
User: "Book the 9am one"
Claude: → calls book_flight(flight_id="...", passenger=context.user)
       ← receives {confirmation: "ABC123"}
       "Booked! Confirmation: ABC123"
```

**Pattern 3: Conditional Branching**
```
User: "Order product X"
Claude: → calls check_inventory(product_id="X")
       ← receives {in_stock: false, eta: "2 days"}
       [branch based on result]
       "Product X is out of stock. Expected back in 2 days.
        Would you like me to notify you when available?"
```

**Pattern 4: Parallel Execution**
```
User: "Compare prices for laptop Y across stores"
Claude: → calls in parallel:
         - check_price(product="Y", store="A")
         - check_price(product="Y", store="B")
         - check_price(product="Y", store="C")
       ← receives all results
       "Here's the comparison:
        Store A: $999
        Store B: $1049
        Store C: $979 (lowest)"
```

**Pattern 5: Iterative/Loop**
```
User: "Find all orders from last month"
Claude: → calls search_orders(month="last", page=1)
       ← receives {orders: [...], has_more: true}
       → calls search_orders(month="last", page=2)
       ← receives {orders: [...], has_more: false}
       [combines results]
       "Found 47 orders from last month..."
```

**Pattern 6: Tool Chain with Validation**
```
User: "Update my email to new@example.com"
Claude: → calls validate_email(email="new@example.com")
       ← receives {valid: true}
       → calls update_user(field="email", value="new@example.com")
       ← receives {success: true}
       "Your email has been updated."
```

---

### Phase 6: Output Generation

**Standard Tool Schema Output:**

```json
{
  "tools": [
    {
      "name": "tool_name",
      "description": "Complete description with usage guidance and return info",
      "input_schema": {
        "type": "object",
        "properties": {
          "param1": {
            "type": "string",
            "description": "Clear parameter description"
          }
        },
        "required": ["param1"]
      }
    }
  ]
}
```

**Implementation Guide Output:**

```markdown
## Tool Implementation Guide

### Tool: [name]

**Purpose:** [What this tool does]

**When Claude Should Use:** [Trigger conditions]

**Input Schema:**
```json
[schema]
```

**Expected Response Format:**
```json
{
  "success": true,
  "data": { ... }
}
```

**Error Handling:**
- [error case]: [how to handle]

**Example Usage:**
```
User: [example query]
Claude calls: [tool with params]
Result: [expected outcome]
```

**Implementation Notes:**
- [Backend requirements]
- [Rate limits]
- [Caching considerations]
```

---

## Tool Design Checklist

### Schema Quality
- [ ] Name is descriptive and snake_case
- [ ] Description explains what, when, and returns
- [ ] All parameters have descriptions
- [ ] Required fields are marked
- [ ] Types are appropriate (string, number, boolean, array, object)
- [ ] Enums used for fixed options
- [ ] Formats specified (dates, IDs, etc.)

### Usability
- [ ] Claude can distinguish between similar tools
- [ ] Tool names imply the action clearly
- [ ] Error responses are informative
- [ ] Partial success is handled
- [ ] Pagination supported for lists

### Reliability
- [ ] Timeout handling defined
- [ ] Retry logic specified
- [ ] Rate limits documented
- [ ] Idempotency considered for mutations

---

## Anti-Patterns to Avoid

### 1. Vague Descriptions
```
BAD: "A tool for data"
GOOD: "Retrieve user profile data including name, email, and preferences. Use when user asks about their account information."
```

### 2. Ambiguous Tool Names
```
BAD: "process", "handle", "do_action"
GOOD: "process_payment", "handle_refund", "create_support_ticket"
```

### 3. Missing Parameter Context
```
BAD: "id": { "type": "string" }
GOOD: "user_id": { "type": "string", "description": "User UUID from authentication context" }
```

### 4. Overlapping Tool Responsibilities
```
BAD: get_user and fetch_user_data (unclear which to use)
GOOD: get_user_profile and get_user_orders (distinct purposes)
```

### 5. Too Many Required Parameters
```
BAD: 10 required parameters (Claude may hallucinate values)
GOOD: Minimal required, sensible defaults for optional
```

---

## Integration with Other Skills

### With prompt-engineer:
- Optimize system prompts for tool-using agents
- Create tool selection guidance in prompts

### With code-review-assistant:
- Review tool implementation code
- Validate error handling patterns

---

## Troubleshooting

### Claude picks wrong tool
- Make descriptions more distinct
- Add "Use this when..." clauses
- Consider combining overlapping tools

### Claude hallucinates parameters
- Add more parameter descriptions
- Reduce required parameters
- Provide format examples in descriptions

### Tool calls fail silently
- Implement clear error responses
- Include error guidance in tool description
- Add retry instructions

### Multi-tool workflows break
- Simplify to fewer tools
- Make dependencies explicit in descriptions
- Consider intermediate confirmation steps

---

## Version History

- v1.0.0 (2025-12-07): Initial release with schema design, orchestration patterns, and implementation guidelines
