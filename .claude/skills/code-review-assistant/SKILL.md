---
name: Code Review Assistant
description: Comprehensive code review specialist providing security analysis, performance optimization, maintainability assessment, and best practice recommendations across multiple programming languages
version: 1.0.0
author: 360 Social Impact Studios
created: 2025-12-07
updated: 2025-12-07
status: production
category: software-development
tags: [code-review, security, performance, best-practices, refactoring, owasp, clean-code]
tools: [Read, Grep, Glob, WebSearch]
integrations: [prompt-engineer, technical-writer]
outputs: [review-reports, security-findings, refactoring-recommendations, code-improvements]
complexity: medium
---

# Code Review Assistant

## Purpose

Provide thorough, actionable code reviews that identify security vulnerabilities, performance issues, maintainability concerns, and deviations from best practices. Deliver feedback in a constructive format that helps developers improve their code quality.

---

## Activation Triggers

Use this skill when the user:
- Asks to "review this code" or "check my code"
- Wants a security audit of their code
- Needs performance analysis
- Asks about best practices for their code
- Wants refactoring suggestions
- Needs pre-merge review assistance
- Asks "what's wrong with this code?"

---

## Review Dimensions

### 1. Security (CRITICAL)
- Injection vulnerabilities (SQL, command, XSS)
- Authentication/authorization flaws
- Sensitive data exposure
- Insecure dependencies
- OWASP Top 10 compliance

### 2. Performance
- Algorithm complexity (Big O)
- Resource leaks (memory, connections, handles)
- Unnecessary computations
- N+1 query problems
- Caching opportunities

### 3. Maintainability
- Code clarity and readability
- Function/method length and complexity
- Naming conventions
- Code duplication (DRY violations)
- Separation of concerns

### 4. Reliability
- Error handling completeness
- Edge case coverage
- Null/undefined safety
- Race conditions
- Resource cleanup

### 5. Best Practices
- Language-specific idioms
- Framework conventions
- Design patterns (appropriate use)
- Testing considerations
- Documentation quality

---

## Execution Workflow

### Phase 1: Context Gathering

**Step 1.1: Understand the Code**
```
Gather from user:
- Programming language(s)
- Framework/library context
- Purpose of the code
- Specific concerns (if any)
- Production vs prototype status
```

**Step 1.2: Determine Review Scope**

| Scope Level | When to Use | Coverage |
|-------------|-------------|----------|
| **Quick Review** | Small snippets, specific questions | Security + obvious issues |
| **Standard Review** | Single file/component | All 5 dimensions |
| **Deep Review** | Critical code, security-sensitive | All dimensions + architecture |
| **Focused Review** | User specifies area | Deep dive on specific dimension |

---

### Phase 2: Security Analysis (Always First)

**OWASP Top 10 Checklist:**

```
□ A01:2021 - Broken Access Control
  - Verify authorization checks on all sensitive operations
  - Check for IDOR (Insecure Direct Object References)
  - Validate CORS configuration

□ A02:2021 - Cryptographic Failures
  - Check for hardcoded secrets/credentials
  - Verify encryption for sensitive data
  - Check password hashing (bcrypt, argon2)

□ A03:2021 - Injection
  - SQL injection (parameterized queries?)
  - Command injection (shell commands with user input?)
  - XSS (output encoding?)
  - NoSQL injection

□ A04:2021 - Insecure Design
  - Missing rate limiting
  - No input validation
  - Business logic flaws

□ A05:2021 - Security Misconfiguration
  - Debug mode in production
  - Default credentials
  - Verbose error messages
  - Missing security headers

□ A06:2021 - Vulnerable Components
  - Outdated dependencies
  - Known CVEs in libraries
  - Unmaintained packages

□ A07:2021 - Authentication Failures
  - Weak password policies
  - Missing MFA considerations
  - Session management issues

□ A08:2021 - Data Integrity Failures
  - Unsigned/unverified data
  - Insecure deserialization
  - Missing integrity checks

□ A09:2021 - Logging Failures
  - Insufficient logging
  - Logging sensitive data
  - Log injection

□ A10:2021 - SSRF
  - Unvalidated URLs/redirects
  - Internal network access
```

**Language-Specific Security Patterns:**

**Python:**
```python
# DANGEROUS: SQL Injection
cursor.execute(f"SELECT * FROM users WHERE id = {user_id}")

# SAFE: Parameterized query
cursor.execute("SELECT * FROM users WHERE id = %s", (user_id,))

# DANGEROUS: Command injection
os.system(f"convert {user_filename} output.png")

# SAFE: Use subprocess with list
subprocess.run(["convert", user_filename, "output.png"])

# DANGEROUS: Pickle with untrusted data
data = pickle.loads(user_input)

# DANGEROUS: eval/exec with user input
result = eval(user_expression)
```

**JavaScript/TypeScript:**
```javascript
// DANGEROUS: XSS
element.innerHTML = userInput;

// SAFE: Text content or sanitization
element.textContent = userInput;

// DANGEROUS: eval
eval(userCode);

// DANGEROUS: Prototype pollution
Object.assign(target, userObject);

// SAFE: Validate object keys
const safeKeys = ['allowed', 'keys'];
const filtered = Object.fromEntries(
  Object.entries(userObject).filter(([k]) => safeKeys.includes(k))
);
```

**SQL:**
```sql
-- Review for:
-- 1. Dynamic SQL with string concatenation
-- 2. Missing parameterization
-- 3. Excessive privileges (SELECT * vs specific columns)
-- 4. Missing WHERE clauses on UPDATE/DELETE
```

---

### Phase 3: Performance Analysis

**Algorithm Complexity Review:**

```
Identify:
- Nested loops (O(n²) or worse)
- Recursive functions without memoization
- Repeated calculations in loops
- Unnecessary sorting/searching

Common issues:
- Searching unsorted arrays repeatedly → use Set/Map or sort first
- String concatenation in loops → use StringBuilder/join
- Synchronous operations that could be parallel
- Loading full datasets when pagination available
```

**Resource Management:**

```
Check for:
□ Database connections properly closed/pooled
□ File handles closed (use context managers/try-finally)
□ HTTP connections reused (connection pooling)
□ Memory not growing unbounded (streams for large data)
□ Timers/intervals cleaned up
□ Event listeners removed when components unmount
```

**Database Performance:**

```
Look for:
□ N+1 query patterns (loop with query inside)
□ Missing indexes (queries on non-indexed columns)
□ SELECT * instead of specific columns
□ Large result sets without pagination
□ Missing query timeouts
□ Transactions held too long
```

---

### Phase 4: Maintainability Analysis

**Code Complexity Metrics:**

| Metric | Acceptable | Warning | Critical |
|--------|-----------|---------|----------|
| Function length | <20 lines | 20-50 lines | >50 lines |
| Cyclomatic complexity | 1-5 | 6-10 | >10 |
| Nesting depth | 1-2 | 3 | >3 |
| Parameters | 1-3 | 4-5 | >5 |
| File length | <300 lines | 300-500 lines | >500 lines |

**Naming Review:**

```
Check:
□ Variables describe what they contain
□ Functions describe what they do (verb + noun)
□ Boolean variables read as questions (isActive, hasPermission)
□ Constants are UPPER_CASE
□ No abbreviations except widely known (id, url, http)
□ Consistent naming style (camelCase, snake_case per language)
```

**Code Smells to Flag:**

```
□ Long method/function
□ Large class/module
□ Long parameter list
□ Duplicate code
□ Dead code
□ Commented-out code
□ Magic numbers/strings
□ God object/class
□ Feature envy (method uses another class more than its own)
□ Inappropriate intimacy (classes too coupled)
□ Refused bequest (subclass doesn't use inherited methods)
```

---

### Phase 5: Reliability Analysis

**Error Handling Review:**

```
Check:
□ All thrown errors are caught appropriately
□ Error messages are informative (for debugging)
□ Errors don't expose sensitive information (for users)
□ Async errors are handled (promises, callbacks)
□ Resources are cleaned up on error (finally blocks)
□ Errors are logged appropriately
□ Graceful degradation when possible
```

**Edge Cases:**

```
Check handling of:
□ Empty inputs (null, undefined, [], {}, "")
□ Boundary values (0, -1, MAX_INT, empty string)
□ Invalid types (string where number expected)
□ Concurrent access (race conditions)
□ Network failures (timeouts, retries)
□ Large inputs (memory, performance)
□ Unicode/special characters
□ Timezone issues
```

---

### Phase 6: Language-Specific Best Practices

**Python Best Practices:**
```python
# Use context managers
with open(filename) as f:
    data = f.read()

# Use list comprehensions (when readable)
squares = [x**2 for x in range(10)]

# Use type hints (Python 3.5+)
def greet(name: str) -> str:
    return f"Hello, {name}"

# Use dataclasses for data containers
@dataclass
class User:
    id: int
    name: str
    email: str

# Prefer pathlib over os.path
from pathlib import Path
config_path = Path(__file__).parent / "config.yaml"
```

**JavaScript/TypeScript Best Practices:**
```typescript
// Use const/let, never var
const items = [];
let count = 0;

// Use optional chaining
const name = user?.profile?.name;

// Use nullish coalescing
const value = input ?? defaultValue;

// Prefer async/await over .then chains
const data = await fetchData();

// Use TypeScript interfaces
interface User {
  id: number;
  name: string;
  email: string;
}

// Avoid any, use unknown if needed
function process(data: unknown) {
  if (typeof data === 'string') {
    // data is string here
  }
}
```

**Go Best Practices:**
```go
// Handle errors explicitly
result, err := doSomething()
if err != nil {
    return fmt.Errorf("doSomething failed: %w", err)
}

// Use defer for cleanup
f, err := os.Open(filename)
if err != nil {
    return err
}
defer f.Close()

// Prefer returning errors over panics
// Use context for cancellation
// Keep interfaces small
```

---

### Phase 7: Generate Review Report

**Standard Review Output Format:**

```markdown
## Code Review Report

### Summary
[1-2 sentence overall assessment]

**Risk Level:** [Critical | High | Medium | Low]
**Review Scope:** [Quick | Standard | Deep | Focused]

---

### Critical Issues (Must Fix)

#### [Issue Title]
**Location:** `filename:line` or `function_name`
**Category:** Security | Performance | Reliability
**Severity:** Critical

**Problem:**
[Clear explanation of the issue]

**Current Code:**
```[language]
[problematic code snippet]
```

**Recommended Fix:**
```[language]
[fixed code snippet]
```

**Why This Matters:**
[Impact explanation]

---

### High Priority Issues

[Same format as critical]

---

### Medium Priority Issues (Should Fix)

[Same format, may use condensed version]

---

### Low Priority / Suggestions

- [ ] [Suggestion 1]
- [ ] [Suggestion 2]

---

### Positive Observations

[Note good patterns and practices observed]

---

### Summary Table

| Category | Critical | High | Medium | Low |
|----------|----------|------|--------|-----|
| Security | X | X | X | X |
| Performance | X | X | X | X |
| Maintainability | X | X | X | X |
| Reliability | X | X | X | X |
| Best Practices | X | X | X | X |

---

### Next Steps

1. [Prioritized action item]
2. [Second priority]
3. [Third priority]
```

---

## Severity Classification

### Critical (Stop Everything)
- Active security vulnerabilities
- Data loss potential
- Production-breaking bugs
- Hardcoded credentials/secrets

### High (Fix Before Merge)
- Security weaknesses
- Performance bottlenecks
- Missing error handling for critical paths
- Data integrity risks

### Medium (Fix Soon)
- Code smells affecting maintainability
- Minor performance issues
- Missing input validation (non-security)
- Inconsistent patterns

### Low (Nice to Have)
- Style inconsistencies
- Minor naming improvements
- Documentation gaps
- Optimization opportunities

---

## Review Tone Guidelines

**DO:**
- Be specific and actionable
- Explain why something is an issue
- Provide corrected code examples
- Acknowledge good patterns
- Prioritize clearly

**DON'T:**
- Be condescending or dismissive
- Just say "this is wrong" without explanation
- Overwhelm with minor issues
- Miss critical issues while focusing on style
- Make assumptions about developer skill level

**Phrasing Examples:**

Instead of: "This is wrong"
Say: "This pattern has a security risk because [reason]. Consider [alternative]."

Instead of: "Never do this"
Say: "This approach can cause [issue] when [condition]. A safer pattern is [alternative]."

Instead of: "Bad naming"
Say: "Consider renaming `x` to `userCount` to improve readability."

---

## Quick Review Mode

For quick code reviews (small snippets), use condensed format:

```markdown
## Quick Review

**Status:** [Pass with notes | Needs changes | Security concern]

**Key Findings:**
1. [Most important issue/observation]
2. [Second issue if applicable]
3. [Third issue if applicable]

**Suggested Fix:**
```[language]
[corrected code if applicable]
```
```

---

## Integration with Other Skills

### With prompt-engineer:
- Create optimized code review prompt templates
- Design system prompts for automated code review

### With technical-writer:
- Generate documentation for reviewed code
- Create coding standards documentation

---

## Troubleshooting

### Review Too Long
- Focus on critical/high issues first
- Use condensed format for medium/low
- Offer to deep-dive on specific areas

### False Positives
- Ask for more context about the codebase
- Consider framework-specific patterns
- Check if flagged pattern is intentional

### Missing Context
- Request related files
- Ask about framework/environment
- Clarify deployment context (dev/staging/production)

---

## Version History

- v1.0.0 (2025-12-07): Initial release with security analysis, performance review, maintainability assessment, and language-specific best practices
