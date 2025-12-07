# Prompt Engineer - Quick Start

## 30-Second Optimization Checklist

- [ ] **Clear task?** Is the instruction unambiguous?
- [ ] **Output format?** Did you specify the expected format?
- [ ] **Constraints?** Length, tone, scope defined?
- [ ] **Role?** Does Claude need expertise context?
- [ ] **Examples?** Complex tasks need 1-2 examples

---

## Optimization Templates

### Simple Task
```
[Action verb] [specific object] [constraints].
```
Example: `Summarize this article in 3 bullet points.`

### Structured Output
```
[Task description]

Return as:
{
  "field1": "type",
  "field2": "type"
}
```

### Expert Role
```
You are a [role] with expertise in [domain].

[Task]

Focus on: [priorities]
Avoid: [exclusions]
```

### Chain-of-Thought
```
[Task] Think step-by-step:
1. First, [step 1]
2. Then, [step 2]
3. Finally, [step 3]
```

---

## Quick Wins

| Issue | Fix |
|-------|-----|
| Too verbose | Remove filler: "please", "I would like", "help me" |
| Inconsistent output | Add explicit format example |
| Wrong focus | Add "Focus on X. Ignore Y." |
| Too long | Specify word/paragraph count |
| Missing context | Add 1-2 sentence background |

---

## Token Reduction Shortcuts

| Verbose | Concise |
|---------|---------|
| "I would like you to" | (delete) |
| "Can you please help me" | (delete) |
| "in a way that is" | (use adjective) |
| "Make sure to" | (use imperative) |
| "It is important that" | "Must:" |

---

## System vs User Message

**System Prompt (persistent rules):**
- Role/persona
- Default format
- Safety rules
- Expertise context

**User Message (per-request):**
- Specific task
- Variable input
- One-time instructions

---

## Common Patterns

**Data Extraction:**
```
Extract [fields] from [content]. Return JSON with null for missing fields.
```

**Code Generation:**
```
Generate [language] code for [task]. Include types and error handling.
```

**Analysis:**
```
Analyze [subject]. Return: Summary, Findings (bulleted), Recommendations (numbered).
```

---

## Troubleshooting

| Problem | Solution |
|---------|----------|
| Ignores instructions | Number them, add "Important:" |
| Adds unwanted caveats | "Respond directly without disclaimers" |
| Inconsistent results | Add 2-3 few-shot examples |
| Wrong format | Show exact output example |
