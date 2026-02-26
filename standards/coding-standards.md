# Coding Standards — [COMPANY_NAME]

> **ระดับ:** Company-wide Baseline
> **ใช้กับ:** ทุกโปรเจกต์ที่ใช้ AI Template นี้
> **เจ้าของ:** Tech Lead / CTO
> **อัปเดตล่าสุด:** [DATE]
> **Version:** 1.0

---

## 1. Universal Principles (ทุกภาษา)

### Clean Code
- **SOLID**: Single Responsibility, Open/Closed, Liskov Substitution, Interface Segregation, Dependency Inversion
- **DRY**: Don't Repeat Yourself — abstract ซ้ำกัน ≥ 3 ครั้ง
- **KISS**: Keep It Simple — อย่าออกแบบสำหรับ use case ที่ยังไม่มี
- **YAGNI**: You Aren't Gonna Need It — ไม่เพิ่ม feature ที่ไม่ได้ใน requirement

### Naming
| ประเภท | Convention | ตัวอย่าง | ภาษา |
|--------|-----------|---------|------|
| Classes / Types / Interfaces | PascalCase | `UserService`, `OrderItem` | ทุกภาษา |
| Methods / Functions | PascalCase | `GetUserById()`, `PlaceOrder()` | **C#** |
| Methods / Functions | camelCase | `getUserById()`, `placeOrder()` | JS/TS, Python |
| Local Variables | camelCase | `userId`, `totalAmount` | C#, JS/TS |
| Local Variables | snake_case | `user_id`, `total_amount` | Python |
| Private Fields (C#) | _camelCase | `_userRepository`, `_logger` | C# เท่านั้น |
| Properties (C#) | PascalCase | `FirstName`, `IsActive` | C# เท่านั้น |
| Constants | UPPER_SNAKE_CASE | `MAX_RETRY_COUNT` | JS/TS, Python |
| Constants (C#) | PascalCase | `MaxRetryCount` | C# เท่านั้น |
| Files (C#) | PascalCase | `UserService.cs`, `OrderController.cs` | C# |
| Files (TypeScript/JS) | kebab-case | `user-service.ts` | JS/TS |
| Files (Python) | snake_case | `user_service.py` | Python |
| Database Tables | snake_case (plural) | `user_orders`, `product_items` | ทุกภาษา |
| API Routes | kebab-case | `/api/v1/cart-items` | ทุกภาษา |
| Environment Variables | UPPER_SNAKE_CASE | `DATABASE_URL`, `JWT_SECRET` | ทุกภาษา |

### Functions
- ฟังก์ชันหนึ่งทำหน้าที่เดียว — ถ้าชื่อต้องใช้ "และ" หรือ "หรือ" → แยกออก
- ไม่เกิน 20 บรรทัด (guideline — ไม่ใช่กฎแข็ง)
- Parameters ≤ 3 ตัว ถ้าเกินให้ใช้ object/struct
- ไม่ส่ง `null` / `undefined` เป็น default behavior — ใช้ Option/Maybe pattern หรือ throw

### Comments
- เขียน comment สำหรับ **"ทำไม"** ไม่ใช่ **"ทำอะไร"**
- Code ที่ดีอธิบายตัวเองได้ — ถ้าต้อง comment ว่า "ทำอะไร" → rename ให้ชัดขึ้นก่อน
- TODO/FIXME ต้องมี ticket reference: `// TODO(PROJ-123): refactor after migration`

---

## 2. Git & Version Control

### Branching Strategy
```
main          ← production-ready เสมอ
develop       ← integration branch (ถ้าใช้ Git Flow)
feature/[ticket-id]-short-description   ← feature branches
bugfix/[ticket-id]-short-description    ← bug fix branches
hotfix/[ticket-id]-short-description    ← production hotfixes
```

### Commit Message Format (Conventional Commits)
```
<type>(<scope>): <short description>

[optional body]

[optional footer: BREAKING CHANGE or closes #issue]
```

**Types:**
| Type | ใช้เมื่อ |
|------|---------|
| `feat` | เพิ่ม feature ใหม่ |
| `fix` | แก้ bug |
| `refactor` | ปรับ code โดยไม่เปลี่ยน behavior |
| `test` | เพิ่ม/แก้ test |
| `docs` | แก้ documentation เท่านั้น |
| `chore` | งาน maintenance (deps update, config) |
| `perf` | ปรับ performance |
| `ci` | แก้ CI/CD config |

**ตัวอย่าง:**
```
feat(cart): add quantity validation before checkout

Prevents checkout when cart item quantity exceeds stock.
Closes #PROJ-456
```

### Pull Request Rules
- PR ต้องมี description บอก: ทำอะไร, ทำไม, วิธี test
- ต้องผ่าน CI (tests + lint) ก่อน merge
- ต้องได้รับ approve ≥ 1 คน (project lead กำหนดเพิ่มได้)
- ห้าม merge ตัวเอง ยกเว้น hotfix และมี approval แล้ว

---

## 3. Testing Standards — Pragmatic TDD

### หลักการ TDD: Red → Green → Refactor

```
🔴 Red    → เขียน failing test จาก Acceptance Criteria ก่อน
            (test ยังรันไม่ผ่าน เพราะ code ยังไม่มี)
🟢 Green  → เขียน code ขั้นต่ำที่สุดที่ทำให้ test ผ่าน
            (ยังไม่ต้องสวยงาม — แค่ pass)
🔵 Refactor → ปรับ code ให้สะอาดขึ้น
              (ต้องมั่นใจว่า test ยังผ่านอยู่หลัง refactor)
```

> **สำคัญ (AI-specific):** เมื่อใช้ AI ช่วยเขียน code ให้แยกเป็น **2 prompt แยกกัน**:
> 1. Prompt แรก: "เขียนเฉพาะ test cases จาก Acceptance Criteria นี้"
> 2. Review + approve test → แล้วค่อย prompt สอง: "เขียน code ให้ test เหล่านี้ผ่าน"
> ห้ามให้ AI เขียน test และ implementation พร้อมกันในครั้งเดียว — นั่นคือ test-after ไม่ใช่ TDD

---

### Pragmatic TDD — ทำ TDD ที่ layer ไหน?

| Layer | TDD? | เหตุผล |
|-------|------|--------|
| **Domain / Business Logic** (Service) | ✅ บังคับ TDD | Core value ของระบบ — ต้องมั่นใจ 100% |
| **Repository / Data Access** | ✅ บังคับ TDD | ใช้ Testcontainers กับ real DB |
| **API Controller / Endpoint** | ⚠️ Test-after ได้ | Integration test หลัง implement ก็เพียงพอ |
| **UI / Frontend Components** | ⚠️ Test-after ได้ | Visual เปลี่ยนบ่อย TDD ไม่คุ้มค่า |
| **Configuration / DI / Startup** | ❌ ไม่ต้อง | Framework รับประกันอยู่แล้ว |
| **DB Migrations** | ❌ ไม่ต้อง | ทดสอบผ่าน Integration tests ของ Repository |

---

### Coverage Requirements

| ประเภท | เป้าหมาย Minimum |
|--------|-----------------|
| Unit Tests (Service/Domain) | ≥ 80% line + branch coverage |
| Integration Tests | Critical paths ครบ 100% |
| E2E Tests | Happy path ทุก user flow |

---

### What to Test

- **Unit (TDD)**: Business logic, validation, data transformation, domain rules — NOT framework code
- **Integration (Test-after)**: API endpoints (request → response), Repository + real DB (Testcontainers)
- **E2E (Test-after)**: User journeys (เช่น login → add to cart → checkout)

---

### Test Naming

**C# (xUnit — primary):**
```csharp
// Pattern: MethodName_Scenario_ExpectedResult
public class OrderServiceTests
{
    // 🔴 เขียนนี้ก่อน — ยังรันไม่ผ่าน
    [Fact]
    public async Task PlaceOrder_WithValidRequest_ReturnsOrderDto() { }

    [Fact]
    public async Task PlaceOrder_WithOutOfStockItem_ThrowsInsufficientStockException() { }

    [Fact]
    public async Task PlaceOrder_WithExpiredCart_ThrowsCartExpiredException() { }

    [Theory]
    [InlineData(0)]
    [InlineData(-1)]
    public async Task PlaceOrder_WithInvalidQuantity_ThrowsValidationException(int qty) { }
}
// 🟢 จากนั้นจึงเขียน OrderService ให้ test เหล่านี้ผ่าน
// 🔵 Refactor OrderService ให้สะอาดขึ้น — test ต้องยังผ่าน
```

**JavaScript/TypeScript (Jest/Vitest — สำหรับ JS services):**
```typescript
// 🔴 เขียน test ก่อน
describe('CartService', () => {
  describe('addItem', () => {
    it('should add item to cart when product is in stock')
    it('should throw InsufficientStockError when quantity exceeds stock')
    it('should throw NotFoundError when product does not exist')
  })
})
// 🟢 จากนั้นเขียน CartService ให้ test ผ่าน
```

---

## 4. Security Baseline

### Mandatory for ALL Projects
- [ ] **Input validation** ที่ boundary ทุกจุด (HTTP, queue, file upload)
- [ ] **Parameterized queries** เท่านั้น — ห้าม string concatenation ใน SQL
- [ ] **Authentication**: JWT หมดอายุใน ≤ 24h (access) + Refresh Token rotation
- [ ] **Password hashing**: bcrypt cost ≥ 12 (≈250ms/hash) หรือ argon2id
- [ ] **Secrets**: ไม่ hardcode ใน code — ใช้ env vars / secrets manager เสมอ
- [ ] **HTTPS**: บังคับ TLS 1.2+ ใน production
- [ ] **Rate limiting**: ทุก public endpoint
- [ ] **Dependency scan**: ก่อน release ทุกครั้ง (`dotnet list package --vulnerable` / npm audit / pip-audit / trivy)

### OWASP Top 10 — Checklist ก่อน Release
- [ ] A01 Broken Access Control
- [ ] A02 Cryptographic Failures
- [ ] A03 Injection (SQL, NoSQL, Command)
- [ ] A05 Security Misconfiguration
- [ ] A07 Identification & Authentication Failures
- [ ] A09 Security Logging & Monitoring

---

## 5. Language-Specific Standards

> **Primary language: C# / .NET 10** — ดู section C# ก่อนเสมอ

### C# / .NET 10 (Primary)

```csharp
// ✅ เปิด Nullable Reference Types ทุก project
// ใส่ใน .csproj: <Nullable>enable</Nullable>

// ✅ ใช้ record สำหรับ immutable DTOs
public record CreateOrderRequest(Guid ProductId, int Quantity, decimal Price);

// ✅ ใช้ async/await ตลอด — ห้าม .Result หรือ .Wait() (deadlock risk)
public async Task<OrderDto> CreateOrderAsync(CreateOrderRequest request, CancellationToken ct)
{
    var order = await _repository.CreateAsync(request, ct);
    return _mapper.Map<OrderDto>(order);
}

// ✅ ใช้ Result pattern หรือ throw custom exceptions — ไม่ return null
// ❌ public Order? GetOrder(Guid id) → return null เมื่อไม่พบ
// ✅ public async Task<Order> GetOrderAsync(Guid id) → throw NotFoundException เมื่อไม่พบ

// ✅ Dependency Injection ผ่าน constructor เสมอ — ไม่ใช้ static/service locator
public class OrderService(IOrderRepository repository, ILogger<OrderService> logger)
{
    private readonly IOrderRepository _repository = repository;
    private readonly ILogger<OrderService> _logger = logger;
}

// ✅ ใช้ IOptions<T> สำหรับ configuration — ไม่อ่าน IConfiguration โดยตรงใน services
// ✅ ใช้ CancellationToken ทุก async method ที่รับ I/O
// ✅ Dispose IDisposable ด้วย using statement หรือ using declaration
// ❌ ห้าม catch (Exception ex) แบบ bare — ระบุ exception type ที่ handle ได้จริง
// ❌ ห้าม string.Format() — ใช้ string interpolation หรือ structured logging แทน
// ❌ ห้าม Thread.Sleep() — ใช้ await Task.Delay() แทน
```

**Project Structure (ASP.NET Core Minimal API):**
```
src/
├── YourProject.Api/          ← Startup, endpoints, middleware
├── YourProject.Application/  ← Use cases, commands/queries (CQRS ถ้าใช้ MediatR)
├── YourProject.Domain/       ← Entities, value objects, domain events
├── YourProject.Infrastructure/ ← EF Core, external services, repositories
└── YourProject.Contracts/    ← DTOs, request/response models (shared)
tests/
├── YourProject.UnitTests/    ← xUnit, Moq/NSubstitute
└── YourProject.IntegrationTests/ ← WebApplicationFactory, Testcontainers
```

**Testing Framework (.NET):**
| Package | ใช้สำหรับ |
|---------|---------|
| **xUnit** | Test framework (default) |
| **FluentAssertions** | Readable assertions |
| **NSubstitute** | Mocking (ใช้แทน Moq สำหรับ project ใหม่) |
| **Testcontainers** | Integration tests กับ real PostgreSQL/Redis |
| **Bogus** | Fake data generation |

**Linting / Code Quality:**
- `dotnet format` — code formatting (รัน pre-commit)
- Roslyn Analyzers: เปิด `<AnalysisMode>All</AnalysisMode>` ใน .csproj
- **SonarAnalyzer.CSharp** — เพิ่มใน CI pipeline

---

### TypeScript / JavaScript
```typescript
// ✅ ใช้ strict TypeScript
{
  "compilerOptions": {
    "strict": true,
    "noImplicitAny": true,
    "strictNullChecks": true
  }
}

// ✅ Prefer async/await over .then() chains
// ✅ ใช้ const โดย default — let เมื่อจำเป็น — ห้าม var
// ✅ ใช้ optional chaining: user?.profile?.avatar
// ✅ ใช้ nullish coalescing: value ?? defaultValue
// ❌ ห้าม any (ยกเว้น migration code ที่มี TODO ชัดเจน)
// ❌ ห้าม console.log ใน production code — ใช้ structured logger
```

**Linting**: ESLint + Prettier (config ใน `.eslintrc` ของโปรเจกต์)

### Python
```python
# ✅ ใช้ Type Hints (PEP 484)
def get_user(user_id: int) -> Optional[User]:
    ...

# ✅ Docstring format: Google Style หรือ NumPy Style (เลือกหนึ่งแบบต่อโปรเจกต์)
# ✅ ใช้ dataclasses หรือ Pydantic สำหรับ data models
# ✅ ใช้ pathlib แทน os.path
# ❌ ห้าม bare except — ระบุ exception type เสมอ
# ❌ ห้าม mutable default arguments: def f(lst=[]) ❌ → def f(lst=None) ✅
```

**Linting**: ruff + mypy (strict mode)

### Go
```go
// ✅ Error handling: ตรวจทุก error — ห้าม ignore ด้วย _
// ✅ ใช้ context.Context ใน I/O functions
// ✅ goroutine ต้องมี done channel หรือ WaitGroup
// ❌ ห้าม panic ใน library code
// ❌ ห้าม global mutable state
```

---

## 6. Code Review Checklist (Summary)

ก่อน approve PR ตรวจ:

- [ ] ตรงตาม requirements
- [ ] ไม่มี logic ซ้ำ (DRY)
- [ ] Error handling ครบ
- [ ] ไม่มี sensitive data ใน log
- [ ] Test ครอบคลุม edge cases
- [ ] ไม่มี hardcoded secrets
- [ ] Performance: ไม่มี N+1 query

---

## 7. การปรับใช้ต่อโปรเจกต์

> **หมายเหตุ:** standards นี้คือ baseline ของบริษัท
> Project-specific overrides ให้บันทึกใน `templates/[project]/tech-stack.md` พร้อมเหตุผล
> ตัวอย่าง: โปรเจกต์บางตัวอาจใช้ coverage ≥ 90% หรือต้องการ 2 approvers

| ข้อ | ค่า Default | Override ได้? |
|-----|------------|--------------|
| Test Coverage | ≥ 80% | ✅ (project กำหนดสูงกว่าได้) |
| PR Approvers | ≥ 1 | ✅ |
| bcrypt cost | ≥ 12 | ❌ (ลดไม่ได้) |
| Parameterized queries | บังคับ | ❌ |
| Secrets in code | ห้าม | ❌ |
