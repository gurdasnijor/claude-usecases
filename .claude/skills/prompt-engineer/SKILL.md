---
name: Prompt Engineer
description: Expert prompt optimization specialist that helps users craft, refine, and optimize prompts for Claude API to maximize effectiveness, reduce token usage, and improve output quality
version: 1.0.0
author: 360 Social Impact Studios
created: 2025-12-07
updated: 2025-12-07
status: production
category: claude-api-optimization
tags: [prompts, optimization, claude-api, tokens, system-prompts, few-shot, chain-of-thought]
tools: [Read, Write, Edit, WebSearch]
integrations: [tool-use-designer, technical-writer]
outputs: [optimized-prompts, prompt-analysis, token-estimates, best-practices]
complexity: medium
---

# Prompt Engineer

## Purpose

Transform user prompts into highly effective Claude API prompts through systematic analysis, optimization, and best practice application. This skill helps developers and teams maximize Claude's capabilities while minimizing token costs.

---

## Activation Triggers

Use this skill when the user:
- Asks to "optimize my prompt" or "improve this prompt"
- Wants to reduce token usage in their Claude API calls
- Needs help crafting system prompts
- Asks about prompt engineering best practices
- Wants to convert a conversational prompt to API format
- Needs few-shot examples or chain-of-thought prompting
- Is debugging why their prompt isn't producing desired outputs

---

## Core Capabilities

### 1. Prompt Analysis
- Identify ambiguities and unclear instructions
- Detect redundant or unnecessary content
- Assess token efficiency
- Evaluate structural clarity
- Check for missing context or constraints

### 2. Prompt Optimization
- Reduce token count while preserving intent
- Improve instruction clarity and specificity
- Add appropriate constraints and guardrails
- Structure for optimal Claude comprehension
- Balance brevity with completeness

### 3. Advanced Techniques
- System prompt architecture
- Few-shot example design
- Chain-of-thought prompting
- Role and persona crafting
- Output format specification
- Error handling instructions

### 4. API-Specific Optimization
- Message role optimization (system/user/assistant)
- Multi-turn conversation design
- Tool use integration
- Streaming considerations
- Temperature and parameter guidance

---

## Execution Workflow

### Phase 1: Intake & Analysis

**Step 1.1: Gather the Prompt**
```
Request from user:
- The current prompt they want to optimize
- The intended use case and context
- Any specific issues they're experiencing
- Desired output format
- Token budget (if applicable)
```

**Step 1.2: Analyze Current Prompt**

Evaluate across these dimensions:

| Dimension | Questions to Assess |
|-----------|---------------------|
| **Clarity** | Is the task unambiguous? Are instructions specific? |
| **Completeness** | Does it include all necessary context? |
| **Constraints** | Are output format, length, and style specified? |
| **Efficiency** | Are there redundant words/phrases? |
| **Structure** | Is information organized logically? |
| **Role Definition** | Is Claude's persona/expertise defined? |

**Step 1.3: Identify Issues**

Common problems to flag:
- Vague or ambiguous language
- Missing output format specification
- Unnecessary verbosity
- Conflicting instructions
- Lack of examples for complex tasks
- Missing edge case handling
- Unclear success criteria

---

### Phase 2: Optimization Strategy

**Step 2.1: Select Optimization Approach**

Based on analysis, choose applicable techniques:

```
IF task is complex or multi-step:
  → Apply chain-of-thought structure
  → Break into numbered steps
  → Add intermediate checkpoints

IF output format is critical:
  → Add explicit format specification
  → Include example output structure
  → Use XML tags or JSON schema

IF task requires expertise:
  → Define Claude's role/persona
  → Specify relevant expertise areas
  → Set appropriate tone and style

IF token budget is tight:
  → Remove filler words and redundancy
  → Use shorthand where unambiguous
  → Consolidate overlapping instructions

IF consistency is important:
  → Add few-shot examples (2-3 typical)
  → Define edge cases explicitly
  → Include "do not" constraints
```

**Step 2.2: Apply the Prompt Framework**

Structure optimized prompts using this template:

```markdown
## System Prompt Structure

[ROLE/PERSONA - 1-2 sentences]
You are [specific expertise]. You [key capability/approach].

[CONTEXT - Only if necessary]
Background: [Relevant context the model needs]

[TASK - Clear and specific]
Your task is to [specific action] given [input type].

[CONSTRAINTS - Explicit boundaries]
Requirements:
- [Requirement 1]
- [Requirement 2]
- [Output format specification]

[EXAMPLES - If needed for complex tasks]
Example input: [sample]
Example output: [sample]

[EDGE CASES - If applicable]
Special handling:
- If [condition], then [action]
- Do not [prohibited action]
```

---

### Phase 3: Optimization Techniques

**Technique 1: Token Reduction**

Before:
```
I would like you to please help me by taking the following text
and summarizing it in a way that captures all of the main points
while also being concise and easy to understand.
```

After:
```
Summarize this text, capturing all main points concisely:
```
*Reduction: 41 tokens → 10 tokens (76% reduction)*

**Technique 2: Specificity Enhancement**

Before:
```
Write something about climate change.
```

After:
```
Write a 200-word executive summary on climate change impacts
for coastal cities, focusing on:
- Sea level rise projections (2030-2050)
- Economic implications
- Adaptation strategies

Format: 3 paragraphs, professional tone, cite recent data.
```

**Technique 3: Output Format Control**

Before:
```
Analyze this data and tell me what you find.
```

After:
~~~
Analyze this dataset and return findings as:

```json
{
  "key_insights": ["insight1", "insight2"],
  "anomalies": [{"field": "", "issue": "", "severity": ""}],
  "recommendations": ["rec1", "rec2"],
  "confidence": "high|medium|low"
}
```
~~~

**Technique 4: Role Definition**

Before:
```
Review this code.
```

After:
```
You are a senior software engineer specializing in Python
with expertise in security, performance, and clean code principles.

Review this code for:
1. Security vulnerabilities (OWASP Top 10)
2. Performance bottlenecks
3. Code maintainability issues

For each issue found, provide:
- Location (line number/function)
- Severity (critical/high/medium/low)
- Specific fix recommendation
```

**Technique 5: Chain-of-Thought**

Before:
```
Solve this math problem: [problem]
```

After:
```
Solve this math problem step-by-step:

1. First, identify what the problem is asking
2. List the known values and unknowns
3. Determine the appropriate formula/approach
4. Show your work for each calculation
5. Verify your answer makes sense
6. State the final answer clearly

Problem: [problem]
```

**Technique 6: Few-Shot Examples**

```
Classify the sentiment of customer reviews.

Examples:
Review: "Absolutely love this product! Works perfectly."
Sentiment: positive

Review: "Broke after one week. Complete waste of money."
Sentiment: negative

Review: "It's okay. Does what it says but nothing special."
Sentiment: neutral

Now classify:
Review: "[user's review]"
Sentiment:
```

---

### Phase 4: API-Specific Optimization

**System vs User Message Allocation**

```python
# Optimal structure for Claude API

messages = [
    {
        "role": "system",
        "content": """You are [role].

        Core instructions that apply to ALL interactions:
        - [Persistent rule 1]
        - [Persistent rule 2]
        - [Output format defaults]
        """
    },
    {
        "role": "user",
        "content": """[Specific task for this request]

        Input: [user's specific input]
        """
    }
]
```

**When to Use System Prompts:**
- Role/persona definition
- Persistent behavioral rules
- Default output formats
- Safety guardrails
- Domain expertise framing

**When to Use User Messages:**
- Specific task requests
- Variable inputs
- One-time instructions
- Dynamic context

**Multi-Turn Optimization**

```python
# Efficient multi-turn pattern

# Turn 1: Establish context
user: "I'm building a Python REST API for user management."

# Turn 2: Specific request (references prior context)
user: "Add input validation to the create_user endpoint we discussed."

# NOT: Repeating all context each turn (token waste)
```

**Tool Use Preparation**

When prompt will involve tools:
```
You have access to the following tools:
- search_database: Query user records
- send_email: Send notifications
- update_record: Modify user data

For each user request:
1. Determine which tool(s) are needed
2. Gather required parameters
3. Execute tools in logical order
4. Synthesize results for the user

Always confirm destructive actions before executing.
```

---

### Phase 5: Deliverables

**Standard Output Format**

```markdown
## Prompt Analysis Report

### Original Prompt
[User's original prompt]

### Issues Identified
1. [Issue 1]: [Explanation]
2. [Issue 2]: [Explanation]

### Optimized Prompt

```
[The optimized prompt]
```

### Optimization Summary
| Metric | Before | After | Improvement |
|--------|--------|-------|-------------|
| Token Count | X | Y | Z% reduction |
| Clarity Score | Low/Med/High | Low/Med/High | [Change] |
| Specificity | Low/Med/High | Low/Med/High | [Change] |

### Techniques Applied
- [Technique 1]: [How it was applied]
- [Technique 2]: [How it was applied]

### Usage Recommendations
- [Recommendation 1]
- [Recommendation 2]
```

---

## Quality Criteria

### Optimized Prompt Must:
- [ ] Be clearer than the original
- [ ] Maintain the user's intent completely
- [ ] Include explicit output format (when applicable)
- [ ] Be appropriately scoped (not over-engineered)
- [ ] Follow Claude API best practices
- [ ] Include constraints where needed

### Token Efficiency Targets:
- Simple prompts: 20-50 tokens
- Standard prompts: 50-150 tokens
- Complex prompts: 150-500 tokens
- System prompts: 100-300 tokens

### Avoid:
- Over-engineering simple requests
- Adding unnecessary constraints
- Removing important context for token savings
- Generic advice without specific improvements

---

## Common Patterns Library

### Pattern: Data Extraction
```
Extract [specific fields] from the following [document type].

Return as JSON:
{
  "field1": "value or null if not found",
  "field2": "value or null if not found",
  "confidence": "high|medium|low"
}

Document:
[content]
```

### Pattern: Code Generation
```
Generate [language] code for [specific functionality].

Requirements:
- [Requirement 1]
- [Requirement 2]

Include:
- Type hints/annotations
- Error handling
- Brief inline comments for complex logic

Do not include:
- Test code (unless requested)
- Excessive comments
- Unused imports
```

### Pattern: Analysis & Recommendations
```
Analyze [subject] and provide actionable recommendations.

Structure your response as:
1. **Current State Summary** (2-3 sentences)
2. **Key Findings** (bulleted list, prioritized)
3. **Recommendations** (numbered, specific actions)
4. **Next Steps** (immediate actions to take)

Focus on [specific aspects]. Ignore [out of scope items].
```

### Pattern: Content Transformation
```
Transform this [input format] into [output format].

Maintain:
- [Element to preserve]
- [Tone/style requirement]

Modify:
- [What should change]
- [Formatting requirement]

Input:
[content]
```

---

## Integration with Other Skills

### With tool-use-designer:
- Optimize prompts that will use Claude tools
- Design tool descriptions for clarity
- Create tool orchestration prompts

### With technical-writer:
- Optimize documentation generation prompts
- Create API documentation prompts
- Design user guide generation prompts

### With code-review-assistant:
- Create code review prompt templates
- Optimize security analysis prompts
- Design refactoring instruction prompts

---

## Troubleshooting

### Issue: Claude ignores instructions
**Solution:** Make instructions more explicit, use numbered lists, add "Important:" prefixes for critical rules

### Issue: Output format inconsistent
**Solution:** Provide explicit format examples, use XML tags or JSON schemas, add format validation instructions

### Issue: Responses too long/short
**Solution:** Specify word/paragraph counts explicitly, use phrases like "in 2-3 sentences" or "comprehensive analysis of 500+ words"

### Issue: Claude adds unwanted caveats
**Solution:** Add instruction "Respond directly without meta-commentary about your limitations"

### Issue: Inconsistent quality across runs
**Solution:** Add few-shot examples, lower temperature, increase specificity of instructions

---

## Version History

- v1.0.0 (2025-12-07): Initial release with core optimization techniques, API patterns, and troubleshooting guide
