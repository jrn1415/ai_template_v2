# Architecture Document — TechShop Online Store
**Version:** 1.0 | **Date:** 2026-03-02 | **Author:** System Architect AI

---

## 1. Architecture Decision

### Pattern: Modular Monolith

**Rationale:**
- Scale ปัจจุบัน (5,000 MAU, 500 concurrent) ไม่ justify complexity ของ microservices
- .NET 10 รองรับ Vertical Slice Architecture ได้ดีในโครงสร้าง monolith
- Single deployment unit ลด operational overhead สำหรับทีมเล็ก
- สามารถ extract เป็น microservices ทีหลังได้ถ้า scale เติบโต

**Alternatives Rejected:**
| Alternative | เหตุผลที่ไม่เลือก |
|-------------|------------------|
| Microservices | Over-engineering สำหรับ team size + scale ปัจจุบัน |
| Serverless | Cold start latency ไม่เหมาะกับ < 500ms NFR |

---

## 2. System Architecture Diagram

```
┌─────────────────────────────────────────────────────────────┐
│                        INTERNET                             │
└──────────────────────────┬──────────────────────────────────┘
                           │ HTTPS
                    ┌──────▼──────┐
                    │  CloudFlare  │  CDN + DDoS Protection
                    │  (CDN/WAF)   │
                    └──────┬──────┘
                           │
              ┌────────────┴────────────┐
              │                         │
       ┌──────▼──────┐          ┌──────▼──────┐
       │  React SPA  │          │  Next.js    │
       │  (Frontend) │          │  (SSR/SEO)  │
       │  Vercel/S3  │          │  (Optional) │
       └──────┬──────┘          └──────┬──────┘
              │                         │
              └────────────┬────────────┘
                           │ REST API / HTTPS
                    ┌──────▼──────┐
                    │  ASP.NET    │
                    │  Core API   │  (.NET 10)
                    │  (Backend)  │
                    └──┬──┬──┬───┘
                       │  │  │
          ┌────────────┘  │  └────────────┐
          │               │               │
   ┌──────▼──────┐  ┌────▼────┐  ┌──────▼──────┐
   │ PostgreSQL  │  │  Redis  │  │  Azure Blob  │
   │  (Primary)  │  │ (Cache) │  │  (Images)   │
   └─────────────┘  └─────────┘  └─────────────┘

External Services:
   ┌─────────────┐  ┌─────────────┐  ┌─────────────┐
   │   Stripe    │  │  PromptPay  │  │  SendGrid   │
   │  (Payment)  │  │    (QR)     │  │   (Email)   │
   └─────────────┘  └─────────────┘  └─────────────┘
```

---

## 3. Tech Stack

| Layer | Technology | Version | Rationale |
|-------|-----------|---------|-----------|
| Frontend | React | 19 | Component ecosystem, hooks, เหมาะกับ SPA |
| Frontend State | Zustand | 5 | Lightweight vs Redux, เพียงพอสำหรับ scale นี้ |
| Frontend Styling | Tailwind CSS | 4 | Utility-first, ไม่ต้องสร้าง design system จาก scratch |
| Backend | ASP.NET Core | .NET 10 | Company standard, strong typing, performance |
| ORM | Entity Framework Core | 9 | .NET standard ORM, migrations built-in |
| Database | PostgreSQL | 16 | ACID, JSON support, strong community |
| Cache | Redis | 7 | Session storage, product catalog cache |
| Image Storage | Azure Blob Storage | — | Cost-effective, CDN integration ดี |
| Auth | JWT + Refresh Tokens | — | Stateless, suitable for SPA |
| Payment | Stripe SDK | latest | PCI-DSS abstraction, PromptPay plugin |
| Email | SendGrid | — | Reliable delivery, template support |
| CDN/WAF | Cloudflare | — | Free tier เพียงพอสำหรับ scale นี้ |
| Container | Docker | 26 | Consistent environments |
| CI/CD | GitHub Actions | — | Free for public, tight GitHub integration |

---

## 4. Backend Module Structure (Vertical Slice)

```
TechShop.API/
├── Modules/
│   ├── Auth/           ← FR-AUTH-001 to FR-AUTH-003
│   │   ├── Commands/   (Register, Login, RefreshToken)
│   │   ├── Queries/    (GetProfile)
│   │   └── Domain/     (User, Role)
│   ├── Products/       ← FR-PROD-001 to FR-PROD-005
│   │   ├── Commands/   (CreateProduct, UpdateProduct, DeleteProduct)
│   │   ├── Queries/    (GetProducts, GetProductById, SearchProducts)
│   │   └── Domain/     (Product, Category, ProductImage)
│   ├── Cart/           ← FR-CART-001, FR-CART-002
│   │   ├── Commands/   (AddToCart, UpdateCartItem, RemoveFromCart)
│   │   ├── Queries/    (GetCart)
│   │   └── Domain/     (Cart, CartItem)
│   ├── Orders/         ← FR-ORD-001 to FR-ORD-005
│   │   ├── Commands/   (CreateOrder, UpdateOrderStatus)
│   │   ├── Queries/    (GetOrders, GetOrderById)
│   │   ├── Services/   (PaymentService, EmailService)
│   │   └── Domain/     (Order, OrderItem, Payment)
│   └── Admin/          ← FR-ADM-001 to FR-ADM-004
│       ├── Commands/   (Admin-specific operations)
│       └── Queries/    (Dashboard, Reports)
├── Infrastructure/
│   ├── Persistence/    (EF Core DbContext, Repositories)
│   ├── Caching/        (Redis implementation)
│   └── ExternalServices/ (Stripe, SendGrid, Azure Blob)
└── Shared/
    ├── Middleware/      (Auth, Error handling, Rate limiting)
    └── Common/          (Result pattern, Pagination)
```

---

## 5. API Design Overview

Base URL: `https://api.techshop.th/v1`

| Method | Endpoint | Description | Auth |
|--------|----------|-------------|------|
| POST | /auth/register | สมัครสมาชิก | Public |
| POST | /auth/login | Login | Public |
| POST | /auth/refresh | Refresh JWT | Public |
| GET | /products | List products (filter/sort/page) | Public |
| GET | /products/{id} | Product detail | Public |
| GET | /cart | Get current cart | Customer |
| POST | /cart/items | Add to cart | Customer |
| PUT | /cart/items/{id} | Update cart item | Customer |
| DELETE | /cart/items/{id} | Remove from cart | Customer |
| POST | /orders | Create order (checkout) | Customer |
| GET | /orders | Order history | Customer |
| GET | /orders/{id} | Order detail + status | Customer |
| POST | /payments/stripe/webhook | Stripe webhook | System |
| POST | /payments/promptpay | Create PromptPay QR | Customer |
| GET | /admin/products | Admin: list products | Admin |
| POST | /admin/products | Admin: create product | Admin |
| PUT | /admin/products/{id} | Admin: update product | Admin |
| GET | /admin/orders | Admin: all orders | Admin |
| PATCH | /admin/orders/{id}/status | Admin: update order status | Admin |

---

## 6. Key Architecture Decisions (ADRs)

### ADR-001: Modular Monolith over Microservices
- **Decision:** Modular Monolith
- **Status:** Accepted
- **Consequences:** ง่ายต่อ deploy + debug, extract เป็น services ได้ทีหลัง

### ADR-002: Redis for Cart + Session
- **Decision:** Redis สำหรับ cart cache และ session
- **Status:** Accepted
- **Consequences:** ต้อง handle Redis downtime gracefully (fallback to DB)

### ADR-003: Stripe Handles PCI Scope
- **Decision:** ไม่เก็บ card data — ใช้ Stripe.js + PaymentIntent
- **Status:** Accepted
- **Consequences:** PCI scope ลดเหลือ SAQ A level

### ADR-004: Optimistic Concurrency for Stock
- **Decision:** EF Core Concurrency Tokens บน `stock_quantity`
- **Status:** Accepted
- **Consequences:** ต้อง handle DbUpdateConcurrencyException ใน checkout flow

---

## Handoff Digest → Role 11: DBA

**Status:** READY

**Critical Items for Next Role:**
- Entities หลัก: User, Product, Category, Cart, CartItem, Order, OrderItem, Payment
- Stock concurrency: ต้องการ row-level locking / optimistic concurrency token บน products.stock_quantity
- Payment: เก็บเฉพาะ payment_intent_id (Stripe), ไม่เก็บ card data
- Session: Cart ของ authenticated users เก็บใน PostgreSQL (ไม่ใช่ Redis เท่านั้น)

**Key Deliverables Created:**
- `templates/02-architecture/architecture-diagram.md` ✅
- `templates/02-architecture/tech-stack.md` ✅
- `templates/02-architecture/api-spec.md` ✅
- `templates/02-architecture/data-flow.md` ✅
