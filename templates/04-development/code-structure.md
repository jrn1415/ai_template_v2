# Code Structure — [SYSTEM_NAME]

**Sprint:** [N]
**Last Updated:** [DATE]
**Author:** Software Developer (Role 4)

> ไฟล์นี้บันทึก folder structure และ module organization ที่ Developer กำหนดไว้
> Role 5 (Code Review) และ Role 6 (Security) ใช้ไฟล์นี้เพื่อเข้าใจโครงสร้างก่อน review

---

## Project Root Structure

```
[project-name]/
├── src/
│   ├── [module-1]/          # [description]
│   ├── [module-2]/          # [description]
│   └── [module-N]/          # [description]
├── tests/
│   ├── unit/
│   └── integration/
├── migrations/              # Database migration files
├── docs/                    # Project-level docs
├── .env.example
├── docker-compose.yml
└── README.md
```

---

## Module Breakdown

### `src/[module-1]/` — [Module Name]

```
[module-1]/
├── [module-1].controller.ts   # HTTP handlers — รับ request, validate, call service
├── [module-1].service.ts      # Business logic — ไม่มี DB calls โดยตรง
├── [module-1].repository.ts   # Database access — SQL/ORM queries
├── [module-1].model.ts        # Type definitions / interfaces
└── [module-1].test.ts         # Unit tests สำหรับ service + repository
```

**Responsibilities:**
- Controller: [รับผิดชอบอะไร]
- Service: [business rules อะไร]
- Repository: [tables ที่ access]

---

### `src/[module-2]/` — [Module Name]

```
[module-2]/
├── [ไฟล์ต่างๆ]
```

**Responsibilities:**
- [description]

---

## Naming Conventions

| ประเภท | Convention | ตัวอย่าง |
|--------|-----------|---------|
| Files | kebab-case | `cart-item.service.ts` |
| Classes | PascalCase | `CartItemService` |
| Functions | camelCase | `addItemToCart()` |
| Constants | UPPER_SNAKE_CASE | `MAX_CART_ITEMS` |
| Database tables | snake_case | `cart_items` |
| API routes | kebab-case | `/api/v1/cart-items` |

---

## Dependencies Between Modules

```
[Module ที่ depend on อะไร]
Controller → Service → Repository → Database
Controller → (does NOT access Repository directly)
```

> **กฎ:** ห้าม Controller เรียก Repository โดยตรง — ต้องผ่าน Service เสมอ

---

## Environment Variables Used

| Variable | Module ที่ใช้ | Purpose |
|----------|-------------|---------|
| `DATABASE_URL` | repository/ | PostgreSQL connection |
| `JWT_SECRET` | auth/ | Token signing |
| `[VAR_NAME]` | [module] | [purpose] |

---

## Sprint History

| Sprint | Modules Added/Modified | Notes |
|--------|----------------------|-------|
| Sprint 1 | [modules] | [เช่น auth + products สร้างใหม่] |
| Sprint 2 | [modules] | [เช่น cart + checkout เพิ่ม] |
