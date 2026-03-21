# Code Review Report — Sprint 1
**Date:** 2026-03-08 | **Reviewer:** Code Review AI | **Sprint:** Foundation & Auth

---

## Review Summary

| Metric | Value |
|--------|-------|
| Files Reviewed | 18 files |
| Issues Found | 0 Critical / 2 Warning / 3 Suggestion |
| Test Coverage | 87% (target: 80%) ✅ |
| Overall Verdict | **APPROVED** |

---

## Acceptance Criteria Check

| Story | AC | Status |
|-------|-----|--------|
| US-001 Register | AC1 (form fields) | PASS |
| US-001 Register | AC2 (validation) | PASS |
| US-001 Register | AC3 (duplicate email) | PASS |
| US-001 Register | AC4 (redirect success) | PASS |
| US-002 Login | AC1 (valid credentials) | PASS |
| US-002 Login | AC2 (wrong credentials) | PASS |
| US-002 Login | AC3 (JWT issued) | PASS |
| US-002 Login | AC4 (auto-refresh) | PASS |
| US-003 Catalog | AC1 (grid + pagination) | PASS |
| US-003 Catalog | AC2 (filter real-time) | PASS |
| US-003 Catalog | AC3 (sort options) | PASS |
| US-003 Catalog | AC4 (search) | PASS |
| US-003 Catalog | AC5 (empty state) | PASS |

---

## Issues Found

### Warning

📍 **Location:** `Modules/Auth/Commands/LoginCommandHandler.cs:42`
🟡 **Severity:** Warning — Timing Attack Risk
📝 **Issue:** เมื่อ user ไม่พบ ระบบ return ทันทีโดยไม่ผ่าน bcrypt.Verify() ซึ่งทำให้ response time ต่างกันระหว่าง "user ไม่มี" กับ "password ผิด" — เปิดช่องทาง timing attack
✅ **Suggestion:** เพิ่ม dummy hash comparison เมื่อ user ไม่พบ:
```csharp
if (user == null)
{
    BCrypt.Net.BCrypt.Verify("dummy", _dummyHash); // constant-time
    return Result.Failure<LoginResponse>("Email หรือรหัสผ่านไม่ถูกต้อง");
}
```
📚 **Reference:** OWASP Authentication Cheat Sheet — Timing Attacks

---

📍 **Location:** `Modules/Products/Queries/GetProductsQueryHandler.cs:28`
🟡 **Severity:** Warning — Missing Cache Invalidation Strategy
📝 **Issue:** Product list ใช้ Redis cache แต่ไม่มีการกำหนด TTL ที่ชัดเจน — ใช้ default ซึ่งอาจ cache ข้อมูล stock เก่า
✅ **Suggestion:** กำหนด TTL ชัดเจน 5 นาทีสำหรับ product list (stock อาจเปลี่ยน):
```csharp
await _cache.SetAsync(cacheKey, products,
    new DistributedCacheEntryOptions
    {
        AbsoluteExpirationRelativeToNow = TimeSpan.FromMinutes(5)
    });
```
📚 **Reference:** Redis Cache-Aside Pattern

---

### Suggestions

📍 **Location:** `Modules/Auth/Domain/User.cs:15`
🟢 **Severity:** Suggestion — XML Documentation Missing
📝 **Issue:** Factory method `Create()` ไม่มี XML doc — ทีมใหม่อาจไม่เข้าใจ reason ของ validation
✅ **Suggestion:** เพิ่ม `/// <summary>` สั้นๆ

---

📍 **Location:** `Infrastructure/Auth/JwtService.cs:8`
🟢 **Severity:** Suggestion — Magic Number
📝 **Issue:** `expiresInMinutes = 60` เป็น magic number
✅ **Suggestion:** Extract เป็น JwtOptions configuration: `_options.AccessTokenExpiryMinutes`

---

📍 **Location:** `Modules/Products/Queries/GetProductsQueryHandler.cs`
🟢 **Severity:** Suggestion — Pagination Default
📝 **Issue:** Default pageSize = 12 hardcoded — ควร configurable
✅ **Suggestion:** ย้ายไป appsettings.json: `"ProductsPageSize": 12`

---

## Test Quality Assessment

| Metric | Result |
|--------|--------|
| Coverage | 87% (lines + branches) ✅ |
| Test naming | `Should_[expected]_When_[condition]` ✅ |
| Shared state | ไม่มี shared state ระหว่าง tests ✅ |
| Mock usage | Appropriate — ไม่ mock ทุกอย่าง ✅ |
| Edge cases | Null input, duplicate email, wrong password ✅ |

**Improvement note:** `LoginCommandHandlerTests.cs` ขาด test สำหรับ inactive user (`is_active = false`) — ควรเพิ่ม

---

## Security Spot Check

| Check | Result |
|-------|--------|
| No hardcoded credentials | ✅ Pass — JWT secret จาก environment variable |
| Input validation | ✅ Pass — FluentValidation บน all endpoints |
| SQL parameterized queries | ✅ Pass — EF Core ทุก query |
| Auth middleware on protected routes | ✅ Pass — `[Authorize]` attribute ครบ |
| Sensitive data not logged | ⚠️ Warning — ดู timing attack issue ด้านบน |

---

## Performance Notes

| Check | Result |
|-------|--------|
| N+1 queries | ✅ None found — EF Core eager loading ใช้ถูกต้อง |
| Pagination | ✅ Products endpoint มี pagination บังคับ (max 50) |
| Missing cache | ⚠️ TTL ไม่ชัดเจน — ดู Warning issue ด้านบน |
| Unnecessary data | ✅ Pass — ไม่มี SELECT * |

---

## Final Verdict

**APPROVED** — 0 Critical, 2 Warnings (non-blocking แต่ควรแก้ใน Sprint นี้)

Sprint 1 code ผ่าน quality bar — ready สำหรับ Security review

---

## Review Checklist

### Correctness
- [x] ทุก AC ถูก implement ครบ
- [x] Business logic ถูกต้อง
- [x] Error handling ครบ (404, 401, 400, 500)

### Code Quality
- [x] SOLID principles ไม่มี major violation
- [x] Function size ≤ 30 lines
- [x] Naming ชัดเจน self-documenting
- [x] Constants ไม่มี magic numbers (minor 2 จุด noted)

### Security
- [x] ไม่มี hardcoded secrets
- [x] Input validation ครบทุก endpoint
- [x] SQL parameterized queries
- [x] Authentication check ถูก endpoint
- [x] Sensitive data ไม่ถูก log

### Testing
- [x] Coverage >= 80% (87%)
- [x] Edge cases covered
- [x] No false positive tests

---

## Handoff Digest → Role 6: Security Engineer

**Status:** READY

**Critical Items for Next Role:**
- Review Verdict: APPROVED
- Sprint: 1 | Coverage: 87%

**Files to Security Scan (priority order):**
1. `Modules/Auth/Commands/LoginCommandHandler.cs` — credential handling + timing attack risk noted
2. `Infrastructure/Auth/JwtService.cs` — token generation
3. `Modules/Auth/Commands/RegisterCommandHandler.cs` — user creation + bcrypt

**Potential Security Concerns for Deep Scan:**
- Timing attack ใน login flow (flagged as Warning)
- JWT secret rotation policy (ยังไม่มี)
- Rate limiting บน /auth/login (มี middleware แต่ยังไม่ verified)

**Key Deliverables Created:**
- `templates/05-code-review/review-report.md` ✅ (รวม Review Checklist ไว้ใน Section ท้าย)
