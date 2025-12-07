# Prompt Engineer

> Expert prompt optimization for Claude API - maximize effectiveness, minimize tokens

## Overview

The Prompt Engineer skill helps developers and teams craft highly effective prompts for Claude API. Whether you're building a production application, reducing costs, or debugging inconsistent outputs, this skill provides systematic optimization techniques.

## When to Use

- **Optimizing existing prompts** for better results or lower token usage
- **Designing system prompts** for Claude-powered applications
- **Debugging prompt issues** like inconsistent outputs or ignored instructions
- **Learning best practices** for Claude API prompt engineering
- **Converting conversational prompts** to production-ready API format

## Key Capabilities

| Capability | Description |
|------------|-------------|
| **Prompt Analysis** | Identify issues with clarity, specificity, and structure |
| **Token Optimization** | Reduce token count while preserving intent (typical 30-70% reduction) |
| **Format Control** | Ensure consistent, structured outputs |
| **Technique Application** | Chain-of-thought, few-shot, role definition, etc. |
| **API Optimization** | System/user message allocation, multi-turn design |

## Quick Examples

### Example 1: Token Reduction

**Before (41 tokens):**
```
I would like you to please help me by taking the following text
and summarizing it in a way that captures all of the main points
while also being concise and easy to understand.
```

**After (10 tokens):**
```
Summarize this text, capturing all main points concisely:
```

### Example 2: Adding Specificity

**Before:**
```
Write something about our product.
```

**After:**
```
Write a 150-word product description for [Product Name].

Include:
- Primary value proposition (1 sentence)
- Three key features with benefits
- Call to action

Tone: Professional but approachable
Audience: Technical decision-makers
```

### Example 3: Output Format Control

**Before:**
```
Analyze this customer feedback.
```

**After:**
```
Analyze this customer feedback and return:

{
  "sentiment": "positive|negative|neutral",
  "key_themes": ["theme1", "theme2"],
  "action_items": ["action1", "action2"],
  "priority": "high|medium|low"
}
```

## Common Optimization Techniques

1. **Role Definition** - Define Claude's expertise and approach
2. **Explicit Constraints** - Specify format, length, tone, scope
3. **Chain-of-Thought** - Break complex tasks into steps
4. **Few-Shot Examples** - Show 2-3 examples for consistency
5. **Negative Instructions** - Specify what NOT to do
6. **Output Schemas** - Use JSON/XML for structured data

## Usage

Simply ask Claude to optimize your prompt:

```
"Optimize this prompt for my Claude API application:
[paste your prompt]

I want to [describe your goal]"
```

Or request specific help:

```
"Help me create a system prompt for a code review assistant
that focuses on security and performance"
```

## Token Efficiency Guidelines

| Prompt Type | Target Token Range |
|-------------|-------------------|
| Simple tasks | 20-50 tokens |
| Standard tasks | 50-150 tokens |
| Complex tasks | 150-500 tokens |
| System prompts | 100-300 tokens |

## Related Skills

- **tool-use-designer** - Design Claude tool schemas
- **technical-writer** - Generate documentation
- **code-review-assistant** - Code analysis prompts

## Version

- **Current:** v1.0.0
- **Last Updated:** 2025-12-07
- **Author:** 360 Social Impact Studios
