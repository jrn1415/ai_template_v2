# Security Report — TechShop Online Store, Sprint 1
**Date:** 2026-03-09 | **Assessor:** Security Engineer AI

---

## Executive Summary

| Metric | Value |
|--------|-------|
| Scope | Auth + Product Catalog (Sprint 1) |
| Critical | 0 |
| High | 1 |
| Medium | 2 |
| Low | 3 |
| Overall Status | **PASSED WITH CONDITIONS** |

**Condition:** High vulnerability ต้องแก้ก่อน Sprint 2 เริ่ม

---

## OWASP Top 10 Assessment

| # | Category | Status | Notes |
|---|----------|--------|-------|
| A01 | Broken Access Control | ✅ Pass | `[Authorize]` attributes ครบ, role check ถูกต้อง |
| A02 | Cryptographic Failures | ⚠️ High | JWT secret rotation ยังไม่มี (ดู SEC-H01) |
| A03 | Injection | ✅ Pass | EF Core parameterized queries ทุกที่ |
| A04 | Insecure Design | ✅ Pass | Input validation + Result pattern ดี |
| A05 | Security Misconfiguration | ✅ Pass | HTTPS enforced, CORS configured correctly |
| A06 | Vulnerable Components | ✅ Pass | ไม่มี known CVEs ใน dependencies |
| A07 | Auth Failures | ⚠️ Medium | Timing attack risk ใน login (ดู SEC-M01) |
| A08 | Software & Data Integrity | ✅ Pass | ไม่มี deserialization ที่ไม่ปลอดภัย |
| A09 | Logging & Monitoring | ⚠️ Medium | Log ขาด security event logging (ดู SEC-M02) |
| A10 | SSRF | ✅ Pass | ไม่มี outbound user-controlled URLs ใน Sprint 1 |

---

## Findings

### SEC-H01 — JWT Secret Rotation Policy ไม่มี
**Severity:** High
**Component:** `Infrastructure/Auth/JwtService.cs`
**Description:** JWT secret ถูก load จาก environment variable ครั้งเดียวตอน startup และไม่มี mechanism สำหรับ rotation หาก secret leaked จะต้อง restart service เพื่อเปลี่ยน key
**Remediation:**
```csharp
// เพิ่ม Key ID (kid) ใน JWT header เพื่อรองรับ rotation
// ใช้ JWKS endpoint pattern หรืออย่างน้อย:
// 1. ตั้ง short expiry (60 min) ✅ already done
// 2. เพิ่ม refresh token blacklist mechanism
// 3. Document JWT rotation runbook
```
**Deadline:** ก่อน Sprint 2

---

### SEC-M01 — Timing Attack ใน Login Flow
**Severity:** Medium (ยืนยันจาก Code Review finding)
**Component:** `LoginCommandHandler.cs:42`
**Description:** Response time ต่างกันระหว่าง "user ไม่มี" vs "password ผิด" อาจใช้ enumerate valid emails ได้
**Remediation:** เพิ่ม dummy bcrypt.Verify() เมื่อ user ไม่พบ (ดูตัวอย่างใน review-report.md)
**Deadline:** Sprint 1 (ก่อน merge)

---

### SEC-M02 — Security Event Logging ไม่ครบ
**Severity:** Medium
**Component:** `AuthController.cs`
**Description:** Failed login attempts ไม่ถูก log พร้อม IP address ทำให้ไม่สามารถ detect brute force attack ได้
**Remediation:**
```csharp
// เพิ่มใน LoginCommandHandler เมื่อ login fail:
_logger.LogWarning(
    "Failed login attempt for email {Email} from IP {IP}",
    command.Email.Mask(), // mask ตรงกลาง
    _httpContextAccessor.HttpContext?.Connection.RemoteIpAddress);
```
**Deadline:** Sprint 1

---

### SEC-L01 — Password Validation ไม่มี Common Password Check
**Severity:** Low
**Component:** `RegisterCommandHandler.cs`
**Description:** Regex validation ตรวจ format แต่ไม่ block passwords ที่พบบ่อย เช่น "Password1!"
**Remediation:** เพิ่ม list of 1000 common passwords หรือ integrate HaveIBeenPwned API
**Deadline:** Could Have (Sprint 3+)

---

### SEC-L02 — Missing HTTP Security Headers
**Severity:** Low
**Component:** `Program.cs` middleware configuration
**Description:** ขาด `X-Content-Type-Options`, `X-Frame-Options`, `Content-Security-Policy` headers
**Remediation:**
```csharp
app.Use(async (context, next) => {
    context.Response.Headers.Add("X-Content-Type-Options", "nosniff");
    context.Response.Headers.Add("X-Frame-Options", "DENY");
    context.Response.Headers.Add("Referrer-Policy", "strict-origin-when-cross-origin");
    await next();
});
```
**Deadline:** Sprint 2

---

### SEC-L03 — Rate Limiting Config Too Permissive
**Severity:** Low
**Component:** `RateLimitingMiddleware.cs`
**Description:** Current limit: 100 requests/minute per IP บน `/auth/login` — ควรเป็น 5-10 requests/minute เพื่อป้องกัน brute force
**Remediation:** ลด limit เป็น 10 requests/minute + exponential backoff
**Deadline:** Sprint 1

---

## Remediation Plan

| ID | Severity | Deadline | Owner | Status |
|----|----------|----------|-------|--------|
| SEC-H01 | High | Before Sprint 2 | Developer | Open |
| SEC-M01 | Medium | Sprint 1 | Developer | Open |
| SEC-M02 | Medium | Sprint 1 | Developer | Open |
| SEC-L01 | Low | Sprint 3+ | Developer | Accepted |
| SEC-L02 | Low | Sprint 2 | Developer | Open |
| SEC-L03 | Low | Sprint 1 | Developer | Open |

---

## Verdict

**PASSED WITH CONDITIONS**

- Sprint 1 ผ่าน security scan
- Developer ต้องแก้ SEC-M01, SEC-M02, SEC-L03 ก่อน Sprint 1 merge
- SEC-H01 ต้องแก้ก่อน Sprint 2 เริ่ม
- SEC-L01 รับ risk ไว้ก่อน (document ใน risk log)

---

## Handoff Digest → Role 7: QA/Tester

**Status:** READY (conditions met by end of Sprint 1)

**Critical Items for Next Role:**
- Security Verdict: PASSED WITH CONDITIONS
- 2 Medium issues flagged สำหรับ regression testing หลัง fix
- Timing attack fix ใน login — ต้องทดสอบว่า response time consistent

**Key Deliverables Created:**
- `templates/06-security/architecture-review.md` ✅ (Phase 1)
- `templates/06-security/threat-model.md` ✅
- `templates/06-security/owasp-assessment.md` ✅
- `templates/06-security/security-report.md` ✅
- `templates/06-security/remediation-plan.md` ✅
