# Requirements Document — TechShop Online Store
**Version:** 1.0 | **Date:** 2026-03-01 | **Author:** Requirements Analyst AI

---

## 1. Project Overview

| Field | Value |
|-------|-------|
| System Name | TechShop Online Store |
| Business Goal | สร้างช่องทางขายอุปกรณ์ IT/Electronics ออนไลน์ รองรับ B2C พร้อม inventory และ order management ครบวงจร |
| Primary Users | ลูกค้าทั่วไป (B2C), Admin |
| Launch Target | Sprint 3 (6 สัปดาห์) |

---

## 2. Functional Requirements

### FR-AUTH: Authentication & Authorization

| ID | Requirement | Priority |
|----|-------------|----------|
| FR-AUTH-001 | ผู้ใช้ลงทะเบียนด้วย email + password | Must Have |
| FR-AUTH-002 | ผู้ใช้ login/logout ด้วย JWT | Must Have |
| FR-AUTH-003 | Admin role แยกจาก Customer role | Must Have |
| FR-AUTH-004 | Password reset ผ่าน email | Should Have |
| FR-AUTH-005 | Social login (Google) | Could Have |

### FR-PRODUCT: Product Catalog

| ID | Requirement | Priority |
|----|-------------|----------|
| FR-PROD-001 | แสดงรายการสินค้าพร้อม pagination | Must Have |
| FR-PROD-002 | Filter สินค้าตาม category, price range, brand | Must Have |
| FR-PROD-003 | Sort สินค้าตาม price, rating, newest | Must Have |
| FR-PROD-004 | Product detail page (images, specs, reviews) | Must Have |
| FR-PROD-005 | Search สินค้าด้วย keyword | Must Have |
| FR-PROD-006 | Product recommendations | Could Have |

### FR-CART: Shopping Cart

| ID | Requirement | Priority |
|----|-------------|----------|
| FR-CART-001 | เพิ่ม/ลบ/แก้จำนวนสินค้าใน cart | Must Have |
| FR-CART-002 | Cart persist ข้าม session (authenticated users) | Must Have |
| FR-CART-003 | Guest cart (ไม่ต้อง login) | Should Have |
| FR-CART-004 | Save for later | Could Have |

### FR-ORDER: Checkout & Orders

| ID | Requirement | Priority |
|----|-------------|----------|
| FR-ORD-001 | Checkout flow: Cart → Shipping → Payment → Confirm | Must Have |
| FR-ORD-002 | ชำระเงินผ่าน Stripe (Credit/Debit card) | Must Have |
| FR-ORD-003 | ชำระเงินผ่าน PromptPay (QR Code) | Must Have |
| FR-ORD-004 | Order confirmation email | Must Have |
| FR-ORD-005 | Order tracking (สถานะ: Pending → Processing → Shipped → Delivered) | Must Have |
| FR-ORD-006 | Order history | Should Have |
| FR-ORD-007 | Cancel order (ก่อน shipped) | Should Have |

### FR-ADMIN: Admin Management

| ID | Requirement | Priority |
|----|-------------|----------|
| FR-ADM-001 | CRUD products (+ upload images) | Must Have |
| FR-ADM-002 | Manage categories | Must Have |
| FR-ADM-003 | View + update order status | Must Have |
| FR-ADM-004 | Inventory management (stock level alerts) | Must Have |
| FR-ADM-005 | Sales dashboard (revenue, top products) | Should Have |
| FR-ADM-006 | Export order reports (CSV) | Could Have |

---

## 3. Non-Functional Requirements

| ID | Category | Requirement | Metric |
|----|----------|-------------|--------|
| NFR-001 | Performance | Page load time | < 2 seconds (P95) |
| NFR-002 | Performance | API response time | < 500ms (P95) |
| NFR-003 | Performance | Concurrent users | 500 users without degradation |
| NFR-004 | Availability | Uptime | 99.5% monthly |
| NFR-005 | Security | Auth | JWT + HTTPS everywhere |
| NFR-006 | Security | Payment | PCI-DSS compliant via Stripe |
| NFR-007 | Usability | Accessibility | WCAG 2.1 AA |
| NFR-008 | Usability | Mobile | Responsive, mobile-first |
| NFR-009 | Usability | Language | Thai + English |
| NFR-010 | Scalability | Database | Handle 1M products |

---

## 4. User Stories

### US-001: User Registration
**As** a new customer
**I want to** create an account with email and password
**So that** I can track my orders and save my cart

**Acceptance Criteria:**
- AC1: ผู้ใช้กรอก email, password, ชื่อ-นามสกุล แล้วกด Register
- AC2: ระบบ validate email format และ password strength (min 8 chars, 1 uppercase, 1 number)
- AC3: ถ้า email ซ้ำ → แสดง error "Email นี้ถูกใช้แล้ว"
- AC4: สมัครสำเร็จ → redirect ไปหน้า home พร้อม welcome message
- AC5: ส่ง verification email (Should Have)

### US-002: User Login
**As** a registered customer
**I want to** login with email and password
**So that** I can access my account and cart

**Acceptance Criteria:**
- AC1: กรอก email + password ถูกต้อง → login สำเร็จ → redirect ไปหน้าก่อนหน้า
- AC2: credentials ผิด → แสดง "Email หรือรหัสผ่านไม่ถูกต้อง" (ไม่ระบุว่าอะไรผิด)
- AC3: Login สำเร็จ → ได้รับ JWT token (access + refresh)
- AC4: JWT expire → auto refresh ถ้า refresh token ยังใช้ได้

### US-003: Product Catalog
**As** a customer
**I want to** browse and search products
**So that** I can find the product I want

**Acceptance Criteria:**
- AC1: หน้า catalog แสดงสินค้าแบบ grid, 12 items/page
- AC2: Filter ตาม category, price range (slider), brand (checkbox) ทำงานแบบ real-time
- AC3: Sort ตาม "ราคาน้อย-มาก", "ราคามาก-น้อย", "ใหม่สุด", "rating สูงสุด"
- AC4: Search bar ค้นหาได้จาก ชื่อสินค้า, brand, description
- AC5: ผลลัพธ์ 0 รายการ → แสดง empty state พร้อม "Clear Filters" button

### US-004: Product Detail
**As** a customer
**I want to** view product details
**So that** I can make an informed purchase decision

**Acceptance Criteria:**
- AC1: แสดง: ชื่อสินค้า, ราคา, รูป (gallery), specs, stock status, reviews
- AC2: ถ้า stock = 0 → ปุ่ม "Add to Cart" disabled + แสดง "สินค้าหมด"
- AC3: ปุ่ม "Add to Cart" เพิ่มสินค้าใน cart และ update cart badge ใน header

### US-005: Shopping Cart
**As** a customer
**I want to** manage my cart
**So that** I can review items before purchasing

**Acceptance Criteria:**
- AC1: แสดงรายการสินค้า, จำนวน, ราคาต่อชิ้น, ราคารวม
- AC2: เพิ่ม/ลด quantity ได้ (min 1, max: stock จำนวน)
- AC3: ลบสินค้าออกจาก cart ได้
- AC4: แสดง subtotal, shipping estimate, total
- AC5: Cart ของ authenticated user คงอยู่ข้าม session

### US-006: Checkout & Payment
**As** a customer
**I want to** checkout and pay for my order
**So that** I can receive my products

**Acceptance Criteria:**
- AC1: Checkout flow: Cart → Shipping address → Payment method → Review → Confirm
- AC2: รองรับ Stripe payment (test mode: card 4242 4242 4242 4242)
- AC3: รองรับ PromptPay (QR Code expires ใน 15 นาที)
- AC4: Payment สำเร็จ → สร้าง Order, ลด stock, ส่ง email confirmation
- AC5: Payment ล้มเหลว → แสดง error message ชัดเจน, cart ยังคงอยู่

---

## 5. Constraints & Assumptions

| Type | Description |
|------|-------------|
| Technical | Backend: .NET 10 (ASP.NET Core), Frontend: React 19 |
| Technical | Database: PostgreSQL 16 |
| Business | Payment: Stripe + PromptPay เท่านั้น (ไม่รับ COD) |
| Business | Shipping: แสดง estimated cost แต่คำนวณนอกระบบ (Phase 1) |
| Assumption | Images host บน cloud storage (S3 / Azure Blob) |
| Assumption | Email service: SendGrid |

---

## 6. Risk Analysis Summary

| Risk | Probability | Impact | Mitigation |
|------|-------------|--------|------------|
| Payment gateway downtime | Low | Critical | Fallback + retry logic, webhook reconciliation |
| Stock oversell (race condition) | Medium | High | Database-level locking / optimistic concurrency |
| Performance ที่ peak load | Medium | High | Caching layer (Redis), pagination บังคับ |
| Security breach (cart/payment) | Low | Critical | HTTPS, parameterized queries, Stripe for PCI scope |

---

## 7. Out of Scope (Won't Have — v1.0)

- Multi-vendor marketplace
- Product subscription / recurring orders
- Real-time chat support
- Native mobile app (iOS/Android)
- Multi-currency (USD only + THB)
- Loyalty points / rewards program

---

## 8. MoSCoW Priority Matrix

### Must Have (Sprint 1-2)

| Feature Area | Stories |
|-------------|---------|
| Authentication | US-001, US-002 |
| Product Catalog | US-003, US-004 |
| Cart | US-005 |
| Checkout + Payment | US-006 |
| Admin: Product + Order | FR-ADM-001, FR-ADM-002, FR-ADM-003, FR-ADM-004 |

### Should Have (Sprint 3)

| Feature Area | Stories |
|-------------|---------|
| Password Reset | FR-AUTH-004 |
| Guest Cart | FR-CART-003 |
| Order History + Cancel | FR-ORD-006, FR-ORD-007 |
| Sales Dashboard | FR-ADM-005 |

### Could Have (Future Sprints)

- Social Login, Save for Later, Product Recommendations, Export Reports

### Won't Have (v1.0)

- Multi-vendor, Subscriptions, Native App, Loyalty Program

---

## 9. Approval

| Stakeholder | Role | Status |
|------------|------|--------|
| Product Owner | Approve requirements | Approved |
| Tech Lead | Technical feasibility | Approved |
| Security | Security requirements | Pending R6 review |

---

## Handoff Digest → Role 2: System Architect

**Status:** READY

**Critical Items for Next Role:**
- Must Have: 14 FRs ครอบคลุม Auth, Product, Cart, Checkout, Admin
- NFRs critical: 500 concurrent users, < 2s page load, HTTPS + JWT, PCI-DSS via Stripe
- Payment: Stripe (card) + PromptPay (QR) — ต้องการ webhook handling
- Race condition risk: Stock เมื่อ multiple users checkout พร้อมกัน

**Open Decisions for Architecture:**
- Monolith vs Microservices (recommend Monolith ก่อน — scale ทีหลัง)
- Caching strategy (Redis vs in-memory)
- Image storage (S3 vs Azure Blob)

**Key Deliverables Created:**
- `templates/01-requirements/requirements-document.md` ✅ (รวม MoSCoW Section 8)
- `templates/01-requirements/user-story-map.md` ✅
- `templates/01-requirements/risk-analysis.md` ✅
