# OWASP Top 10 Assessment

## Project: [SYSTEM_NAME]
**Assessment Date**: [DATE]
**Assessor**: Security Engineer

---

## A01: Broken Access Control

| Check | Status | Finding | Remediation |
|-------|--------|---------|-------------|
| Enforce least privilege | Pass/Fail | [detail] | [action] |
| Deny by default | Pass/Fail | | |
| CORS properly configured | Pass/Fail | | |
| Directory listing disabled | Pass/Fail | | |
| Rate limiting on API | Pass/Fail | | |
| JWT token validation | Pass/Fail | | |
| Resource ownership verified | Pass/Fail | | |

**Risk Level**: Critical / High / Medium / Low / None

---

## A02: Cryptographic Failures

| Check | Status | Finding | Remediation |
|-------|--------|---------|-------------|
| Data classified (sensitive vs public) | Pass/Fail | | |
| Sensitive data encrypted at rest | Pass/Fail | | |
| TLS in transit (v1.2+) | Pass/Fail | | |
| Strong algorithms used (no MD5/SHA1) | Pass/Fail | | |
| Keys properly managed | Pass/Fail | | |
| Passwords hashed (bcrypt/argon2) | Pass/Fail | | |

**Risk Level**: Critical / High / Medium / Low / None

---

## A03: Injection

| Check | Status | Finding | Remediation |
|-------|--------|---------|-------------|
| SQL parameterized queries | Pass/Fail | | |
| NoSQL injection prevention | Pass/Fail | | |
| Command injection prevention | Pass/Fail | | |
| ORM used properly | Pass/Fail | | |
| Input validation (allowlist) | Pass/Fail | | |
| Output encoding | Pass/Fail | | |

**Risk Level**: Critical / High / Medium / Low / None

---

## A04: Insecure Design

| Check | Status | Finding | Remediation |
|-------|--------|---------|-------------|
| Threat modeling performed | Pass/Fail | | |
| Security in design phase | Pass/Fail | | |
| Unit/integration security tests | Pass/Fail | | |
| Business logic abuse prevention | Pass/Fail | | |
| Resource limits defined | Pass/Fail | | |

**Risk Level**: Critical / High / Medium / Low / None

---

## A05: Security Misconfiguration

| Check | Status | Finding | Remediation |
|-------|--------|---------|-------------|
| Unnecessary features disabled | Pass/Fail | | |
| Default credentials changed | Pass/Fail | | |
| Error handling configured | Pass/Fail | | |
| Security headers set | Pass/Fail | | |
| Software up to date | Pass/Fail | | |
| Cloud permissions minimal | Pass/Fail | | |

**Risk Level**: Critical / High / Medium / Low / None

---

## A06: Vulnerable & Outdated Components

| Check | Status | Finding | Remediation |
|-------|--------|---------|-------------|
| Dependencies scanned | Pass/Fail | | |
| No known vulnerabilities | Pass/Fail | | |
| Unused dependencies removed | Pass/Fail | | |
| Update plan in place | Pass/Fail | | |

**Risk Level**: Critical / High / Medium / Low / None

---

## A07: Identification & Authentication Failures

| Check | Status | Finding | Remediation |
|-------|--------|---------|-------------|
| Brute force protection | Pass/Fail | | |
| Strong password policy | Pass/Fail | | |
| MFA available | Pass/Fail | | |
| Session management secure | Pass/Fail | | |
| Token rotation implemented | Pass/Fail | | |

**Risk Level**: Critical / High / Medium / Low / None

---

## A08: Software & Data Integrity Failures

| Check | Status | Finding | Remediation |
|-------|--------|---------|-------------|
| CI/CD pipeline secured | Pass/Fail | | |
| Dependency integrity verified | Pass/Fail | | |
| Unsigned data not trusted | Pass/Fail | | |
| Code review required | Pass/Fail | | |

**Risk Level**: Critical / High / Medium / Low / None

---

## A09: Security Logging & Monitoring Failures

| Check | Status | Finding | Remediation |
|-------|--------|---------|-------------|
| Authentication events logged | Pass/Fail | | |
| Access control failures logged | Pass/Fail | | |
| Log integrity protected | Pass/Fail | | |
| Alerting configured | Pass/Fail | | |
| Incident response plan exists | Pass/Fail | | |

**Risk Level**: Critical / High / Medium / Low / None

---

## A10: Server-Side Request Forgery (SSRF)

| Check | Status | Finding | Remediation |
|-------|--------|---------|-------------|
| URL validation (allowlist) | Pass/Fail | | |
| Internal network access blocked | Pass/Fail | | |
| Metadata endpoint protection | Pass/Fail | | |
| Raw responses not returned | Pass/Fail | | |

**Risk Level**: Critical / High / Medium / Low / None

---

## Overall Assessment

| Category | Risk Level | Findings | Open Issues |
|----------|-----------|----------|-------------|
| A01 | | [X] | [X] |
| A02 | | [X] | [X] |
| A03 | | [X] | [X] |
| A04 | | [X] | [X] |
| A05 | | [X] | [X] |
| A06 | | [X] | [X] |
| A07 | | [X] | [X] |
| A08 | | [X] | [X] |
| A09 | | [X] | [X] |
| A10 | | [X] | [X] |
| **Overall** | **[LEVEL]** | **[X]** | **[X]** |
