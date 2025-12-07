# Code Review Assistant - Quick Start

## Request a Review

```
Review this [language] code:
[paste code]
```

Optional context:
```
Review this code for [security/performance/all].
It's a [description] for [use case].
```

---

## Severity Quick Reference

| Level | Icon | Action |
|-------|------|--------|
| Critical | :no_entry: | Fix immediately |
| High | :warning: | Fix before merge |
| Medium | :wrench: | Fix soon |
| Low | :eyes: | Nice to have |

---

## Security Checklist (OWASP Top 10)

- [ ] **A01: Broken Access Control** - Authorization checks? IDOR?
- [ ] **A02: Cryptographic Failures** - Secrets hardcoded? Encryption?
- [ ] **A03: Injection** - Parameterized queries? Input sanitized?
- [ ] **A05: Security Misconfiguration** - Debug mode? Default creds?
- [ ] **A07: Authentication Failures** - Password hashing? Session management?

---

## Performance Red Flags

| Pattern | Problem | Fix |
|---------|---------|-----|
| Nested loops | O(n²) | Use maps/sets |
| Query in loop | N+1 problem | Batch/join |
| No connection pool | Resource exhaustion | Pool connections |
| `SELECT *` | Over-fetching | Select specific columns |
| String concat in loop | Memory churn | StringBuilder/join |

---

## Code Smells Quick Check

- [ ] Function >20 lines?
- [ ] Nesting >3 levels deep?
- [ ] >5 parameters?
- [ ] Magic numbers/strings?
- [ ] Duplicate code blocks?
- [ ] Commented-out code?
- [ ] Generic names (temp, data, x)?

---

## Language-Specific Dangers

**Python:**
```python
# SQL Injection
f"SELECT * FROM users WHERE id = {user_id}"  # BAD

# Command Injection
os.system(f"convert {filename}")  # BAD

# Unsafe deserialization
pickle.loads(user_input)  # BAD
```

**JavaScript:**
```javascript
// XSS
element.innerHTML = userInput;  // BAD

// Eval
eval(userCode);  // BAD

// Prototype pollution
Object.assign(targetObject, userObject);  // RISKY
```

---

## Quick Review Output

```
Status: [Pass | Needs Changes | Security Concern]

Key Findings:
1. [Issue]
2. [Issue]

Fix:
[code example]
```

---

## Full Review Output

```
Summary: [assessment]
Risk Level: [Critical/High/Medium/Low]

Critical Issues:
- [Issue with fix]

High Priority:
- [Issue with fix]

Medium/Low:
- [Suggestions]

Next Steps:
1. [Action]
2. [Action]
```
