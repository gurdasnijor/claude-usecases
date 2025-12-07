---
name: Security Audit Assistant
description: Comprehensive security specialist that performs vulnerability assessments, secure code reviews, dependency audits, and provides remediation guidance following OWASP, CWE, and industry security standards
version: 1.0.0
author: 360 Social Impact Studios
created: 2025-12-07
updated: 2025-12-07
status: production
category: security
tags: [security, owasp, vulnerability, audit, secure-coding, penetration-testing, compliance]
tools: [Read, Write, Edit, Glob, Grep, Bash, WebSearch]
integrations: [code-review-assistant, cicd-pipeline-designer]
outputs: [security-reports, vulnerability-assessments, remediation-guides, compliance-checklists]
complexity: high
---

# Security Audit Assistant

## Purpose

Perform comprehensive security assessments of applications, infrastructure, and code. Identify vulnerabilities, assess risk levels, and provide actionable remediation guidance following industry security standards.

---

## Activation Triggers

Use this skill when the user:
- Asks for a "security audit" or "security review"
- Needs "vulnerability assessment"
- Wants to check for "OWASP vulnerabilities"
- Asks about "secure coding" practices
- Needs "dependency security" analysis
- Wants "penetration testing" guidance
- Asks about "security compliance"

---

## Security Frameworks

### Primary
- **OWASP Top 10** (Web Application Security)
- **CWE/SANS Top 25** (Software Weaknesses)
- **NIST Cybersecurity Framework**

### Compliance Standards
- SOC 2
- PCI DSS (Payment Card Industry)
- HIPAA (Healthcare)
- GDPR (Data Privacy)

---

## Execution Workflow

### Phase 1: Scope Definition

**Step 1.1: Define Audit Scope**

```
Determine:
- What type of system? (Web app, API, mobile, infrastructure)
- What technologies? (Languages, frameworks, databases)
- What's in scope? (Code, dependencies, config, infrastructure)
- What compliance requirements? (SOC 2, PCI, HIPAA)
- What's the threat model? (Who are the attackers?)
```

**Step 1.2: Audit Types**

| Type | Focus | Deliverable |
|------|-------|-------------|
| **Code Review** | Source code vulnerabilities | Vulnerability report |
| **Dependency Audit** | Third-party library risks | CVE report |
| **Configuration Review** | Misconfigurations | Hardening guide |
| **Architecture Review** | Design flaws | Threat model |
| **Penetration Test** | Exploitable vulnerabilities | Pentest report |

---

### Phase 2: OWASP Top 10 Assessment

**A01:2021 - Broken Access Control**

```
Check for:
□ Missing authorization checks on sensitive endpoints
□ IDOR (Insecure Direct Object References)
□ Path traversal vulnerabilities
□ CORS misconfiguration
□ JWT validation issues
□ Privilege escalation paths

Indicators:
- Direct object references without access checks
- Missing role/permission validation
- Predictable resource IDs
```

**Testing Examples:**
```python
# VULNERABLE: No authorization check
@app.get("/users/{user_id}")
def get_user(user_id: int):
    return db.get_user(user_id)  # Any user can access any profile

# SECURE: Authorization check
@app.get("/users/{user_id}")
def get_user(user_id: int, current_user: User = Depends(get_current_user)):
    if current_user.id != user_id and not current_user.is_admin:
        raise HTTPException(403, "Forbidden")
    return db.get_user(user_id)
```

---

**A02:2021 - Cryptographic Failures**

```
Check for:
□ Sensitive data transmitted in cleartext
□ Weak encryption algorithms (MD5, SHA1, DES)
□ Hardcoded secrets/credentials
□ Missing encryption at rest
□ Weak key management
□ Improper certificate validation

Indicators:
- HTTP instead of HTTPS
- Passwords stored in plaintext or weak hashes
- API keys in source code
- Self-signed certificates in production
```

**Secure Patterns:**
```python
# Password hashing
from argon2 import PasswordHasher
ph = PasswordHasher()
hashed = ph.hash(password)
ph.verify(hashed, password)  # Verification

# Secrets management
import os
api_key = os.environ.get("API_KEY")  # NOT in code

# Encryption
from cryptography.fernet import Fernet
key = Fernet.generate_key()  # Store securely
cipher = Fernet(key)
encrypted = cipher.encrypt(data.encode())
```

---

**A03:2021 - Injection**

```
Check for:
□ SQL injection
□ NoSQL injection
□ Command injection
□ LDAP injection
□ XPath injection
□ Template injection

Indicators:
- String concatenation with user input
- Dynamic query construction
- User input in shell commands
```

**Testing Examples:**
```python
# SQL Injection
# VULNERABLE
query = f"SELECT * FROM users WHERE id = {user_input}"

# SECURE
query = "SELECT * FROM users WHERE id = %s"
cursor.execute(query, (user_input,))

# Command Injection
# VULNERABLE
os.system(f"convert {user_filename} output.png")

# SECURE
subprocess.run(["convert", user_filename, "output.png"], check=True)

# Template Injection (SSTI)
# VULNERABLE (Jinja2)
template = Template(user_input)

# SECURE
template = Template("Hello {{ name }}")
template.render(name=user_input)
```

---

**A04:2021 - Insecure Design**

```
Check for:
□ Missing rate limiting
□ No account lockout
□ Lack of input validation
□ Missing CAPTCHA for sensitive operations
□ Insufficient anti-automation
□ Business logic flaws

Design Requirements:
- Defense in depth
- Least privilege
- Fail securely
- Separation of duties
```

---

**A05:2021 - Security Misconfiguration**

```
Check for:
□ Default credentials
□ Unnecessary services enabled
□ Debug mode in production
□ Missing security headers
□ Verbose error messages
□ Directory listing enabled
□ Outdated software

Security Headers Checklist:
□ Content-Security-Policy
□ X-Content-Type-Options: nosniff
□ X-Frame-Options: DENY
□ Strict-Transport-Security
□ X-XSS-Protection (legacy)
□ Referrer-Policy
```

**Header Implementation:**
```python
# Flask
@app.after_request
def add_security_headers(response):
    response.headers['X-Content-Type-Options'] = 'nosniff'
    response.headers['X-Frame-Options'] = 'DENY'
    response.headers['Content-Security-Policy'] = "default-src 'self'"
    response.headers['Strict-Transport-Security'] = 'max-age=31536000; includeSubDomains'
    return response
```

---

**A06:2021 - Vulnerable and Outdated Components**

```
Check for:
□ Known CVEs in dependencies
□ Outdated libraries/frameworks
□ Unmaintained packages
□ Components with known vulnerabilities

Tools:
- npm audit (Node.js)
- pip-audit (Python)
- cargo audit (Rust)
- OWASP Dependency-Check
- Snyk, Dependabot
```

**Dependency Audit Commands:**
```bash
# Node.js
npm audit
npm audit fix
npm outdated

# Python
pip-audit
safety check -r requirements.txt

# Go
go list -m all | nancy sleuth

# Rust
cargo audit
```

---

**A07:2021 - Identification and Authentication Failures**

```
Check for:
□ Weak password policies
□ Missing brute force protection
□ Credential stuffing vulnerability
□ Session fixation
□ Insecure session management
□ Missing MFA options
□ Password in URL parameters

Password Policy Minimums:
- Minimum 12 characters
- Complexity not required (NIST 800-63B)
- Check against breach databases
- No password hints
- Secure password reset flow
```

**Session Security:**
```python
# Secure session configuration
app.config['SESSION_COOKIE_SECURE'] = True  # HTTPS only
app.config['SESSION_COOKIE_HTTPONLY'] = True  # No JS access
app.config['SESSION_COOKIE_SAMESITE'] = 'Lax'  # CSRF protection
app.config['PERMANENT_SESSION_LIFETIME'] = timedelta(hours=1)
```

---

**A08:2021 - Software and Data Integrity Failures**

```
Check for:
□ Untrusted deserialization
□ Missing integrity verification
□ Insecure CI/CD pipelines
□ Auto-update without verification
□ Unsigned code/packages

Secure Practices:
- Verify digital signatures
- Use SRI for CDN resources
- Lock dependency versions
- Sign commits and releases
```

---

**A09:2021 - Security Logging and Monitoring Failures**

```
Check for:
□ Insufficient logging of security events
□ Logs not protected from tampering
□ No alerting for security incidents
□ Missing audit trails
□ Log injection vulnerabilities

What to Log:
- Authentication attempts (success/failure)
- Authorization failures
- Input validation failures
- Security exceptions
- Admin actions
- Data access patterns
```

**Logging Best Practices:**
```python
import logging

# Structured logging
logger.info("User login", extra={
    "event_type": "authentication",
    "user_id": user_id,
    "ip_address": request.remote_addr,
    "success": True,
    "timestamp": datetime.utcnow().isoformat()
})

# Don't log sensitive data
# BAD: logger.info(f"User password: {password}")
# GOOD: logger.info(f"Password changed for user {user_id}")
```

---

**A10:2021 - Server-Side Request Forgery (SSRF)**

```
Check for:
□ User-controlled URLs fetched server-side
□ Internal network access via application
□ Cloud metadata endpoint access
□ File:// and other protocol access

Mitigations:
- Allowlist domains/IPs
- Block internal IP ranges
- Disable unnecessary protocols
- Use network segmentation
```

**SSRF Prevention:**
```python
import ipaddress
from urllib.parse import urlparse

def is_safe_url(url):
    parsed = urlparse(url)

    # Only allow http/https
    if parsed.scheme not in ['http', 'https']:
        return False

    # Block internal IPs
    try:
        ip = ipaddress.ip_address(parsed.hostname)
        if ip.is_private or ip.is_loopback or ip.is_reserved:
            return False
    except ValueError:
        pass  # It's a hostname, not IP

    # Allowlist check
    allowed_domains = ['api.example.com', 'cdn.example.com']
    if parsed.hostname not in allowed_domains:
        return False

    return True
```

---

### Phase 3: Dependency Security

**Step 3.1: Dependency Audit Process**

```bash
# 1. Generate dependency list
npm list --all --json > dependencies.json  # Node
pip freeze > requirements.txt  # Python

# 2. Check for vulnerabilities
npm audit --json > npm-audit.json
pip-audit --output-json > pip-audit.json

# 3. Review high/critical issues
# 4. Update or replace vulnerable packages
# 5. Document accepted risks
```

**Step 3.2: Vulnerability Prioritization**

| CVSS Score | Severity | Action Timeline |
|------------|----------|-----------------|
| 9.0 - 10.0 | Critical | Immediate (24h) |
| 7.0 - 8.9 | High | Within 1 week |
| 4.0 - 6.9 | Medium | Within 1 month |
| 0.1 - 3.9 | Low | Next release |

---

### Phase 4: Security Report Generation

**Step 4.1: Vulnerability Report Template**

```markdown
# Security Audit Report

**Application:** [Name]
**Version:** [Version]
**Audit Date:** [Date]
**Auditor:** [Name/Team]
**Scope:** [What was reviewed]

## Executive Summary

[2-3 paragraph overview for non-technical stakeholders]

**Risk Rating:** [Critical/High/Medium/Low]
**Total Vulnerabilities:** [Count]
- Critical: [X]
- High: [X]
- Medium: [X]
- Low: [X]

## Critical Findings

### [VULN-001] [Vulnerability Title]

**Severity:** Critical (CVSS: 9.8)
**Category:** A03:2021 - Injection
**CWE:** CWE-89 SQL Injection
**Location:** `src/api/users.py:45`

**Description:**
[Detailed explanation of the vulnerability]

**Evidence:**
```python
# Vulnerable code
query = f"SELECT * FROM users WHERE id = {request.args.get('id')}"
```

**Impact:**
- Unauthorized data access
- Data modification/deletion
- Potential system compromise

**Remediation:**
```python
# Fixed code
query = "SELECT * FROM users WHERE id = %s"
cursor.execute(query, (request.args.get('id'),))
```

**References:**
- [OWASP SQL Injection](https://owasp.org/Top10/A03_2021-Injection/)
- [CWE-89](https://cwe.mitre.org/data/definitions/89.html)

---

## High Findings
[Same format as Critical]

## Medium Findings
[Condensed format]

## Low Findings
[List format]

---

## Recommendations Summary

| Priority | Finding | Effort | Impact |
|----------|---------|--------|--------|
| 1 | Fix SQL injection | Low | Critical |
| 2 | Update dependencies | Medium | High |
| 3 | Add security headers | Low | Medium |

## Remediation Timeline

| Phase | Findings | Target Date |
|-------|----------|-------------|
| Immediate | Critical | [Date] |
| Short-term | High | [Date + 1 week] |
| Medium-term | Medium | [Date + 1 month] |
| Long-term | Low | [Next release] |

## Appendices

### A. Methodology
[Testing approach and tools used]

### B. Scope Limitations
[What was not tested and why]

### C. Tool Output
[Raw tool outputs if applicable]
```

---

### Phase 5: Remediation Guidance

**Quick Fixes by Vulnerability Type:**

| Vulnerability | Quick Fix |
|---------------|-----------|
| SQL Injection | Use parameterized queries |
| XSS | HTML-encode output |
| CSRF | Add CSRF tokens |
| Path Traversal | Validate/sanitize paths |
| Open Redirect | Allowlist redirect URLs |
| Insecure Cookies | Set Secure, HttpOnly, SameSite |
| Missing Headers | Add security headers |
| Weak Passwords | Implement password policy |

**Security Headers Implementation:**
```nginx
# Nginx configuration
add_header X-Content-Type-Options "nosniff" always;
add_header X-Frame-Options "DENY" always;
add_header X-XSS-Protection "1; mode=block" always;
add_header Content-Security-Policy "default-src 'self'" always;
add_header Strict-Transport-Security "max-age=31536000; includeSubDomains" always;
add_header Referrer-Policy "strict-origin-when-cross-origin" always;
add_header Permissions-Policy "geolocation=(), microphone=(), camera=()" always;
```

---

## Security Checklist

### Application Security
- [ ] Input validation on all user inputs
- [ ] Output encoding for XSS prevention
- [ ] Parameterized queries for SQL
- [ ] CSRF protection enabled
- [ ] Secure session management
- [ ] Proper error handling (no stack traces)
- [ ] Security headers configured
- [ ] Rate limiting implemented

### Authentication & Authorization
- [ ] Strong password policy
- [ ] Brute force protection
- [ ] Secure password reset
- [ ] MFA available for sensitive accounts
- [ ] Authorization checks on all endpoints
- [ ] Principle of least privilege

### Data Protection
- [ ] Encryption in transit (TLS 1.2+)
- [ ] Encryption at rest for sensitive data
- [ ] No secrets in code/config files
- [ ] Proper key management
- [ ] Data classification implemented

### Infrastructure
- [ ] Firewall configured
- [ ] Unnecessary ports closed
- [ ] OS and services patched
- [ ] Logging and monitoring enabled
- [ ] Backups tested and encrypted

---

## Integration with Other Skills

### With code-review-assistant:
- Comprehensive code review with security focus
- Identify security issues during development

### With cicd-pipeline-designer:
- Add security scanning to CI/CD
- Implement SAST/DAST automation

---

## Troubleshooting

### False positives in scans
- Review tool configuration
- Whitelist known safe patterns
- Validate manually before dismissing

### Overwhelming number of findings
- Prioritize by CVSS score
- Focus on critical/high first
- Group similar issues

### Legacy code challenges
- Prioritize publicly exposed code
- Add compensating controls
- Plan gradual remediation

---

## Version History

- v1.0.0 (2025-12-07): Initial release with OWASP Top 10 assessment, dependency auditing, and remediation guidance
