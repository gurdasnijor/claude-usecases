# Code Review Assistant

> Comprehensive code review covering security, performance, maintainability, and best practices

## Overview

The Code Review Assistant provides thorough, actionable code reviews across multiple programming languages. It identifies security vulnerabilities, performance issues, maintainability concerns, and deviations from best practices.

## When to Use

- **Pre-merge reviews** - Catch issues before code reaches production
- **Security audits** - Identify OWASP Top 10 vulnerabilities
- **Performance analysis** - Find bottlenecks and resource leaks
- **Code quality assessment** - Evaluate maintainability and readability
- **Learning** - Understand best practices for your language/framework

## Review Dimensions

| Dimension | Focus Areas |
|-----------|-------------|
| **Security** | Injection, auth, data exposure, OWASP Top 10 |
| **Performance** | Complexity, resource leaks, N+1 queries, caching |
| **Maintainability** | Readability, naming, duplication, complexity |
| **Reliability** | Error handling, edge cases, race conditions |
| **Best Practices** | Language idioms, framework conventions, patterns |

## Languages Supported

- Python
- JavaScript/TypeScript
- Go
- SQL
- Java
- Rust
- C/C++
- Ruby
- PHP
- And more...

## Usage Examples

### Basic Review
```
Review this code:

[paste your code]
```

### Focused Review
```
Review this code for security vulnerabilities only:

[paste your code]
```

### With Context
```
Review this Python Flask endpoint. It's for a financial application
handling user account balances:

[paste your code]
```

## Severity Levels

| Level | Meaning | Action |
|-------|---------|--------|
| **Critical** | Active vulnerability, data loss risk | Stop and fix immediately |
| **High** | Security weakness, major bugs | Fix before merge |
| **Medium** | Code smells, minor issues | Fix soon |
| **Low** | Style, documentation | Nice to have |

## Output Format

Reviews are structured as:
1. **Summary** - Overall assessment and risk level
2. **Critical Issues** - Must-fix problems with code examples
3. **High Priority** - Important issues to address
4. **Medium/Low** - Suggestions for improvement
5. **Positive Observations** - Good patterns noted
6. **Next Steps** - Prioritized action items

## Security Checks (OWASP Top 10)

- A01: Broken Access Control
- A02: Cryptographic Failures
- A03: Injection (SQL, XSS, Command)
- A04: Insecure Design
- A05: Security Misconfiguration
- A06: Vulnerable Components
- A07: Authentication Failures
- A08: Data Integrity Failures
- A09: Logging Failures
- A10: SSRF

## Quick Review Mode

For small snippets, get a condensed review:

```
Quick review:

[paste short code snippet]
```

Returns pass/fail status with 1-3 key findings.

## Related Skills

- **prompt-engineer** - Create code review prompt templates
- **technical-writer** - Document coding standards

## Version

- **Current:** v1.0.0
- **Last Updated:** 2025-12-07
- **Author:** 360 Social Impact Studios
