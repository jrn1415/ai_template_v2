# Threat Model (STRIDE)

## Project: [SYSTEM_NAME]

---

## System Scope

| Component | Description | Trust Level |
|-----------|-------------|-------------|
| [Web App] | Frontend application | Untrusted |
| [API Server] | Backend service | Trusted |
| [Database] | Data storage | Trusted |
| [External API] | Third-party service | Semi-trusted |

## Data Flow Diagram

```
┌──────────┐     HTTPS      ┌───────────┐     TCP       ┌──────────┐
│  Client  │ ──────────────→ │ API Server│ ────────────→ │ Database │
│ (Browser)│ ←────────────── │           │ ←──────────── │          │
└──────────┘                 └───────────┘               └──────────┘
                                  │
                                  │ HTTPS
                                  ▼
                             ┌───────────┐
                             │ External  │
                             │ Service   │
                             └───────────┘

Trust Boundary: ═══════════════════════════
```

## STRIDE Analysis

### S - Spoofing (การปลอมตัว)

| # | Threat | Component | Impact | Likelihood | Mitigation |
|---|--------|-----------|--------|------------|------------|
| S-1 | User impersonation via stolen credentials | Auth | High | Medium | MFA, session management |
| S-2 | API key theft | API Gateway | High | Low | Key rotation, IP whitelist |
| S-3 | | | | | |

### T - Tampering (การแก้ไขข้อมูล)

| # | Threat | Component | Impact | Likelihood | Mitigation |
|---|--------|-----------|--------|------------|------------|
| T-1 | Request body manipulation | API | High | Medium | Input validation, HMAC signing |
| T-2 | Database injection | Database | Critical | Medium | Parameterized queries, ORM |
| T-3 | | | | | |

### R - Repudiation (การปฏิเสธการกระทำ)

| # | Threat | Component | Impact | Likelihood | Mitigation |
|---|--------|-----------|--------|------------|------------|
| R-1 | User denies performing action | All | Medium | Medium | Audit logging, timestamps |
| R-2 | | | | | |

### I - Information Disclosure (การรั่วไหลของข้อมูล)

| # | Threat | Component | Impact | Likelihood | Mitigation |
|---|--------|-----------|--------|------------|------------|
| I-1 | Error messages expose internals | API | Medium | High | Generic error responses |
| I-2 | Sensitive data in logs | Logging | High | Medium | Log sanitization |
| I-3 | | | | | |

### D - Denial of Service

| # | Threat | Component | Impact | Likelihood | Mitigation |
|---|--------|-----------|--------|------------|------------|
| D-1 | API flood attack | API Gateway | High | Medium | Rate limiting, WAF |
| D-2 | Large payload upload | API | Medium | Medium | Request size limits |
| D-3 | | | | | |

### E - Elevation of Privilege (การยกระดับสิทธิ์)

| # | Threat | Component | Impact | Likelihood | Mitigation |
|---|--------|-----------|--------|------------|------------|
| E-1 | Horizontal privilege escalation | API | Critical | Medium | Resource ownership checks |
| E-2 | Vertical privilege escalation | Auth | Critical | Low | Role verification middleware |
| E-3 | | | | | |

---

## Risk Matrix Summary

| Threat ID | Risk Score | Priority | Status |
|-----------|-----------|----------|--------|
| S-1 | High | P1 | Open |
| T-2 | Critical | P0 | Open |
| | | | |
