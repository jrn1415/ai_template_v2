# Security Policies & Best Practices

## Project: [SYSTEM_NAME]

---

## 1. Input Validation

```
Rule: Validate ALL input at system boundaries

- Use allowlist validation (not blocklist)
- Validate data type, length, range, format
- Sanitize before processing
- Reject invalid input (don't try to fix it)
```

| Input Type | Validation Rules |
|-----------|-----------------|
| Email | RFC 5322 format, max 255 chars |
| Password | Min 8 chars, uppercase, lowercase, number, special |
| Username | Alphanumeric + underscore, 3-30 chars |
| Phone | E.164 format |
| URL | HTTPS only, allowlisted domains |
| File Upload | Allowlisted MIME types, max size [X]MB |
| Free Text | Max length, HTML escape output |

## 2. Authentication Policy

| Policy | Requirement |
|--------|------------|
| Password Minimum Length | 8 characters |
| Password Complexity | Upper + Lower + Number + Special |
| Password History | Last 5 passwords |
| Account Lockout | After 5 failed attempts |
| Lockout Duration | 15 minutes (progressive) |
| Session Timeout | 30 minutes (idle) |
| Session Absolute Timeout | 8 hours |
| MFA | Required for admin, optional for users |
| Token Expiry | Access: 15 min, Refresh: 7 days |

## 3. Authorization Policy

```
Principle: Least Privilege + Deny by Default
```

| Role | Permissions |
|------|-----------|
| Admin | Full access |
| Manager | Read/Write own org, Read reports |
| User | Read/Write own data only |
| Guest | Read public data only |

## 4. Data Classification

| Level | Label | Examples | Handling |
|-------|-------|---------|----------|
| L4 | Restricted | Passwords, tokens, keys | Encrypted, no logs, minimal access |
| L3 | Confidential | PII, financial data | Encrypted, audit logged |
| L2 | Internal | Business data, configs | Access controlled |
| L1 | Public | Marketing, docs | No restrictions |

## 5. API Security Headers

```
Strict-Transport-Security: max-age=31536000; includeSubDomains
Content-Security-Policy: default-src 'self'; script-src 'self'
X-Content-Type-Options: nosniff
X-Frame-Options: DENY
X-XSS-Protection: 0
Referrer-Policy: strict-origin-when-cross-origin
Permissions-Policy: camera=(), microphone=(), geolocation=()
```

## 6. CORS Policy

```
Allowed Origins: [specific domains only]
Allowed Methods: GET, POST, PUT, PATCH, DELETE
Allowed Headers: Content-Type, Authorization
Credentials: true (only for trusted origins)
Max Age: 3600
```

## 7. Rate Limiting

| Endpoint Category | Limit | Window | Action on Exceed |
|-------------------|-------|--------|-----------------|
| Authentication | 10 req | 1 min | 429 + lockout |
| API Read | 100 req | 1 min | 429 + retry-after |
| API Write | 30 req | 1 min | 429 + retry-after |
| File Upload | 5 req | 1 min | 429 |

## 8. Logging Requirements

**Must Log:**
- Authentication events (success/failure)
- Authorization failures
- Input validation failures
- System errors
- Data access (CRUD) for sensitive data
- Admin actions

**Must NOT Log:**
- Passwords or secrets
- Full credit card numbers
- Session tokens
- PII beyond user ID
