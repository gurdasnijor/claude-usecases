# Security Audit Assistant

> Comprehensive security assessments, vulnerability identification, and remediation guidance

## Overview

The Security Audit Assistant performs thorough security assessments of applications and infrastructure. It identifies vulnerabilities using OWASP Top 10 and other security standards, then provides actionable remediation guidance.

## When to Use

- **Security audits** - Comprehensive vulnerability assessment
- **Code reviews** - Security-focused code analysis
- **Dependency checks** - CVE scanning for third-party libraries
- **Compliance prep** - SOC 2, PCI DSS, HIPAA readiness
- **Penetration testing** - Vulnerability identification guidance

## Security Frameworks

| Framework | Focus |
|-----------|-------|
| **OWASP Top 10** | Web application vulnerabilities |
| **CWE Top 25** | Common software weaknesses |
| **NIST CSF** | Cybersecurity framework |
| **PCI DSS** | Payment card security |
| **SOC 2** | Service organization controls |

## Quick Example

**Request:**
```
Perform a security audit on this Flask API endpoint:
[paste code]
```

**Output:**
```markdown
## Security Findings

### CRITICAL: SQL Injection (A03:2021)
**Location:** `api/users.py:45`
**CVSS:** 9.8

**Vulnerable Code:**
```python
query = f"SELECT * FROM users WHERE id = {user_id}"
```

**Fix:**
```python
query = "SELECT * FROM users WHERE id = %s"
cursor.execute(query, (user_id,))
```
```

## OWASP Top 10 (2021)

| ID | Category | Example |
|----|----------|---------|
| A01 | Broken Access Control | Missing authz checks |
| A02 | Cryptographic Failures | Weak hashing |
| A03 | Injection | SQL, command injection |
| A04 | Insecure Design | No rate limiting |
| A05 | Security Misconfiguration | Debug mode on |
| A06 | Vulnerable Components | Outdated dependencies |
| A07 | Authentication Failures | Weak passwords |
| A08 | Data Integrity Failures | Insecure deserialization |
| A09 | Logging Failures | Missing audit trails |
| A10 | SSRF | Unvalidated URLs |

## Severity Ratings

| CVSS | Severity | Timeline |
|------|----------|----------|
| 9.0-10.0 | Critical | 24 hours |
| 7.0-8.9 | High | 1 week |
| 4.0-6.9 | Medium | 1 month |
| 0.1-3.9 | Low | Next release |

## Dependency Auditing

```bash
# Node.js
npm audit

# Python
pip-audit

# Go
go list -m all | nancy

# Rust
cargo audit
```

## Related Skills

- **code-review-assistant** - Security in code reviews
- **cicd-pipeline-designer** - Automated security scanning

## Version

- **Current:** v1.0.0
- **Last Updated:** 2025-12-07
- **Author:** 360 Social Impact Studios
