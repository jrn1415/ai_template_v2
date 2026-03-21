# Architecture Security Review

## Project: [SYSTEM_NAME]
**Date**: [DATE]
**Reviewer**: Security Engineer
**Mode**: Phase 1 — Architecture Review

---

## Executive Summary

[2-3 sentences summarizing the review result]

**Review Verdict**: APPROVED / ISSUES FOUND

| Severity | Count |
|----------|-------|
| Critical | [X] |
| High | [X] |
| Medium | [X] |
| Low | [X] |

**Recommendation**: PROCEED to R3+R4 / RETURN to R2

---

## 1. Architecture Threat Assessment (STRIDE)

> Architecture-level threat analysis — design decisions, not source code

### Component: [API Gateway / Auth Service / Database / External Integration]

| Threat | Attack Vector | Impact | Likelihood | Current Design Mitigation | Gaps |
|--------|--------------|--------|------------|--------------------------|------|
| **S**poofing | [how] | H/M/L | H/M/L | [mitigation] | [gap] |
| **T**ampering | [how] | H/M/L | H/M/L | [mitigation] | [gap] |
| **R**epudiation | [how] | H/M/L | H/M/L | [mitigation] | [gap] |
| **I**nformation Disclosure | [how] | H/M/L | H/M/L | [mitigation] | [gap] |
| **D**enial of Service | [how] | H/M/L | H/M/L | [mitigation] | [gap] |
| **E**levation of Privilege | [how] | H/M/L | H/M/L | [mitigation] | [gap] |

*(Repeat for each critical component)*

---

## 2. Authentication & Authorization Architecture Review

| Check | Status | Notes |
|-------|--------|-------|
| Auth mechanism appropriate for use case | Pass/Fail | [details] |
| RBAC/ABAC design correct | Pass/Fail | [details] |
| Session management plan | Pass/Fail | [details] |
| Token strategy (JWT/OAuth) | Pass/Fail | [details] |
| MFA consideration | Pass/Fail | [details] |

---

## 3. Data Security Architecture

| Check | Status | Notes |
|-------|--------|-------|
| Sensitive data identified | Pass/Fail | [list of sensitive data types] |
| Encryption at rest planned | Pass/Fail | [algorithm + scope] |
| Encryption in transit planned | Pass/Fail | [TLS version] |
| PII handling approach | Pass/Fail | [PDPA/GDPR compliance] |
| Secrets management plan | Pass/Fail | [approach] |
| Backup encryption | Pass/Fail | [details] |

---

## 4. API & Network Security Design

| Check | Status | Notes |
|-------|--------|-------|
| CORS policy defined | Pass/Fail | [allowed origins] |
| Rate limiting planned | Pass/Fail | [limits per endpoint type] |
| HTTPS enforcement | Pass/Fail | [TLS version] |
| API versioning strategy | Pass/Fail | [approach] |
| Input validation strategy | Pass/Fail | [whitelist/blacklist] |
| Security headers planned | Pass/Fail | [CSP, X-Frame-Options, etc.] |

---

## 5. Security Gaps & Recommendations

| # | Gap | Severity | Recommendation | Owner |
|---|-----|----------|---------------|-------|
| 1 | [description] | Critical/High/Medium/Low | [specific recommendation] | R2/R4 |
| 2 | [description] | Critical/High/Medium/Low | [specific recommendation] | R2/R4 |

---

## 6. Handoff Digest

### If APPROVED → Handoff to Role 3 (UX/UI) + Role 4 (Developer)

**Security Constraints for Role 3 (UX/UI):**
- [constraint 1]
- [constraint 2]

**Security Constraints for Role 4 (Developer):**
- [constraint 1]
- [constraint 2]

### If ISSUES FOUND → Return to Role 2 (System Architect)

**Items to fix in Architecture:**
1. [Critical/High gap + specific recommendation]
2. [Critical/High gap + specific recommendation]
