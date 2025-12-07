# Security Audit Assistant - Quick Start

## Request Security Audit

```
Perform security audit on:
[paste code or describe system]

Focus: [OWASP/dependencies/all]
```

---

## OWASP Top 10 Quick Check

- [ ] **A01: Access Control** - Auth checks on all endpoints?
- [ ] **A02: Crypto** - Strong hashing? No hardcoded secrets?
- [ ] **A03: Injection** - Parameterized queries?
- [ ] **A05: Misconfiguration** - Debug off? Headers set?
- [ ] **A06: Dependencies** - No known CVEs?
- [ ] **A07: Authentication** - Strong passwords? Lockout?

---

## Common Vulnerabilities

**SQL Injection:**
```python
# BAD
query = f"SELECT * FROM users WHERE id = {user_id}"

# GOOD
cursor.execute("SELECT * FROM users WHERE id = %s", (user_id,))
```

**XSS:**
```javascript
// BAD
element.innerHTML = userInput;

// GOOD
element.textContent = userInput;
```

**Command Injection:**
```python
# BAD
os.system(f"convert {filename}")

# GOOD
subprocess.run(["convert", filename])
```

---

## Dependency Audit

```bash
# Node.js
npm audit

# Python
pip-audit

# Check severity
npm audit --audit-level=high
```

---

## Security Headers

```
X-Content-Type-Options: nosniff
X-Frame-Options: DENY
Content-Security-Policy: default-src 'self'
Strict-Transport-Security: max-age=31536000
```

---

## Severity Quick Reference

| CVSS | Severity | Fix By |
|------|----------|--------|
| 9-10 | Critical | 24h |
| 7-8.9 | High | 1 week |
| 4-6.9 | Medium | 1 month |
| 0-3.9 | Low | Next release |

---

## Report Template

```markdown
## Finding: [Title]
**Severity:** [Critical/High/Medium/Low]
**Category:** [OWASP ID]
**Location:** [file:line]

**Issue:** [Description]

**Fix:**
[code example]
```

---

## Quick Fixes

| Issue | Fix |
|-------|-----|
| SQL Injection | Parameterized queries |
| XSS | HTML encode output |
| CSRF | Add CSRF tokens |
| Weak passwords | 12+ chars, breach check |
| Missing headers | Add security headers |
