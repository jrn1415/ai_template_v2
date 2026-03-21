# Wireframes — TechShop Online Store
**Version:** 1.0 | **Date:** 2026-03-04 | **Author:** UX/UI Designer AI

---

## Screen Inventory

| # | Screen | Route | Role |
|---|--------|-------|------|
| 1 | Home / Landing | / | All |
| 2 | Product Listing | /products | All |
| 3 | Product Detail | /products/:id | All |
| 4 | Cart | /cart | All |
| 5 | Checkout — Shipping | /checkout/shipping | Customer |
| 6 | Checkout — Payment | /checkout/payment | Customer |
| 7 | Order Confirmation | /orders/:id/confirmation | Customer |
| 8 | Order Tracking | /orders/:id | Customer |
| 9 | Login | /login | Guest |
| 10 | Register | /register | Guest |
| 11 | Admin — Products | /admin/products | Admin |
| 12 | Admin — Orders | /admin/orders | Admin |

---

## Screen 1: Product Listing

```
Route: /products
Purpose: แสดงรายการสินค้าพร้อม filter/sort/search

+--[Header: TechShop Logo | Search Bar | Cart(3) | Login]--+
|                                                           |
| [Breadcrumb: Home > Storage]                              |
|                                                           |
| ┌─────────────────────────────────────────────────────┐  |
| │ FILTER SIDEBAR (20%)  │ PRODUCT GRID (80%)          │  |
| │                       │                             │  |
| │ [Category]            │ Sort: [Price ▼] [12 items]  │  |
| │ ☑ Storage (24)        │                             │  |
| │ ☐ RAM (18)            │ [IMG][IMG][IMG]             │  |
| │ ☐ CPU (12)            │ [Name][Name][Name]          │  |
| │                       │ [Price][Price][Price]       │  |
| │ [Price Range]         │ ★4.5  ★4.2  ★4.8            │  |
| │ ฿500 ──●── ฿20,000    │ [Add Cart][Add Cart][Add]   │  |
| │                       │                             │  |
| │ [Brand]               │ [IMG][IMG][IMG]             │  |
| │ ☑ Samsung (8)         │ [Name][Name][Name]          │  |
| │ ☐ WD (6)              │ [Price][Price][Price]       │  |
| │ ☐ Seagate (5)         │ [Add Cart][Add Cart][Add]   │  |
| │                       │                             │  |
| │ [Rating]              │ [Pagination: ← 1 2 3 →]     │  |
| │ ⭐⭐⭐⭐☆ (15+)          │                             │  |
| └─────────────────────────────────────────────────────┘  |
+-----------------------------------------------------------+

States:
- Loading: Skeleton cards (3x3 grid) + filter skeleton
- Empty: "ไม่พบสินค้า '[keyword]'" + [Clear Filters] button + suggested products
- Error: "ไม่สามารถโหลดสินค้าได้" + [ลองอีกครั้ง] button
- Filter active: Active filters appear as removable chips above grid
```

---

## Screen 2: Product Detail

```
Route: /products/:id
Purpose: แสดงรายละเอียดสินค้าและ Add to Cart

+--[Header]--+
|                                                           |
| [Breadcrumb: Home > Storage > Samsung 980 Pro]            |
|                                                           |
| ┌──────────────────────┬──────────────────────────────┐  |
| │  IMAGE GALLERY (50%) │  PRODUCT INFO (50%)           │  |
| │                      │                               │  |
| │  [Main Image]        │  Samsung 980 Pro 1TB NVMe    │  |
| │                      │  ⭐⭐⭐⭐⭐ (4.8) 128 reviews   │  |
| │  [Thumb][Thumb][Thm] │                               │  |
| │                      │  ฿3,499                       │  |
| │                      │  ~~฿3,999~~ (12% off)         │  |
| │                      │                               │  |
| │                      │  ✅ In Stock (23 remaining)   │  |
| │                      │                               │  |
| │                      │  Qty: [−] [1] [+]            │  |
| │                      │                               │  |
| │                      │  [🛒 Add to Cart]  [♡ Save]   │  |
| └──────────────────────┴──────────────────────────────┘  |
|                                                           |
| [Tabs: Description | Specs | Reviews]                     |
|                                                           |
| [Specs Content]                                           |
| Read Speed: 7,000 MB/s | Write Speed: 6,500 MB/s         |
|                                                           |
| [Related Products]                                        |
+-----------------------------------------------------------+

States:
- Loading: Skeleton layout (image placeholder + info skeleton)
- Out of Stock: stock_quantity = 0 →
    "สินค้าหมดชั่วคราว" badge + [Add to Cart] disabled + [แจ้งเตือนเมื่อมีสินค้า] button
- Error: "ไม่พบสินค้านี้" + [กลับหน้าสินค้า] link
```

---

## Screen 3: Shopping Cart

```
Route: /cart
Purpose: Review และแก้ไข cart ก่อน checkout

+--[Header]--+
|                                                           |
| Shopping Cart (3 items)                                   |
|                                                           |
| ┌─────────────────────────────────────┬─────────────┐   |
| │ CART ITEMS (70%)                    │ SUMMARY(30%)│   |
| │                                     │             │   |
| │ [IMG] Samsung 980 Pro 1TB           │ Subtotal    │   |
| │       ฿3,499    Qty:[−][1][+]  [🗑] │ ฿8,997      │   |
| │ ─────────────────────────────────── │             │   |
| │ [IMG] Corsair 16GB DDR5 RAM         │ Shipping    │   |
| │       ฿2,299    Qty:[−][2][+]  [🗑] │ ฿99         │   |
| │ ─────────────────────────────────── │             │   |
| │ [IMG] Logitech MX Master 3S         │ Total       │   |
| │       ฿3,199    Qty:[−][1][+]  [🗑] │ ฿9,096      │   |
| │                                     │             │   |
| │                                     │ [Checkout→] │   |
| │                                     │             │   |
| │                                     │ Or          │   |
| └─────────────────────────────────────┘ [Continue   │   |
|                                          Shopping]   │   |
+-----------------------------------------------------------+

States:
- Loading: Skeleton rows
- Empty Cart: ภาพ cart ว่าง + "ตะกร้าของคุณว่างเปล่า" + [เริ่มช้อปปิ้ง] button
- Quantity > Stock: แสดง warning "สินค้าเหลือเพียง X ชิ้น" ปรับ qty อัตโนมัติ
- Item out of stock (ระหว่าง session): แสดง warning row + [Remove] button
```

---

## Screen 4: Checkout — Payment

```
Route: /checkout/payment
Purpose: เลือก payment method และยืนยันการชำระ

+--[Header: ขั้นตอน: 1.Cart → 2.Shipping → 3.Payment → 4.Confirm]--+
|                                                                    |
| Payment Method                                                     |
|                                                                    |
| ┌─── Credit/Debit Card ─────────────────────────────┐            |
| │ ○ Credit/Debit Card                               │            |
| │   [  4242  ] [  4242  ] [  4242  ] [  4242  ]     │            |
| │   [Cardholder Name    ]  [MM/YY] [CVV]            │            |
| │   🔒 Secured by Stripe                             │            |
| └────────────────────────────────────────────────────┘            |
|                                                                    |
| ┌─── PromptPay ──────────────────────────────────────┐            |
| │ ● PromptPay (QR Code)                              │            |
| │   [QR CODE IMAGE]                                  │            |
| │   ฿9,096 — หมดอายุใน 14:32                        │            |
| │   สแกนด้วย banking app ใดก็ได้                    │            |
| └────────────────────────────────────────────────────┘            |
|                                                                    |
| Order Summary:                                                     |
| Samsung 980 Pro x1 = ฿3,499 | Corsair RAM x2 = ฿4,598            |
| Subtotal: ฿8,997 | Shipping: ฿99 | **Total: ฿9,096**               |
|                                                                    |
| [← แก้ไขที่อยู่]                    [ยืนยันและชำระ →]             |
+--------------------------------------------------------------------+

States:
- Processing payment: overlay spinner + "กำลังดำเนินการ..." + ห้ามกดซ้ำ
- Payment Success: → redirect to /orders/:id/confirmation
- Payment Failed: Error banner "การชำระเงินไม่สำเร็จ: [reason]" + [ลองอีกครั้ง]
  cart ยังคงอยู่ครบถ้วน
- PromptPay timeout: "QR หมดอายุ" + [สร้าง QR ใหม่] button
```

---

## Screen 5: Admin — Product Management

```
Route: /admin/products
Purpose: Admin จัดการรายการสินค้าทั้งหมด

+--[Admin Sidebar Nav]--+--[Main Content]--+
| Dashboard             |                  |
| ► Products            | Products (247)   [+ Add Product]
| Orders                |                  |
| Categories            | [Search...]  Filter: [All ▼] [Active ▼]
| Settings              |                  |
|                       | ID | ชื่อ | ราคา | Stock | Status | Actions |
|                       | ──────────────────────────────────────── |
|                       | [img] Sam 980 | 3,499 |  23  | Active | [✏][🗑]|
|                       | [img] DDR5 16G | 2,299 |  0  | OOS    | [✏][🗑]|
|                       | [img] MX Master| 3,199 |   5  | Active | [✏][🗑]|
|                       |                  |
|                       | [Pagination: ← 1 2 … 21 →]               |
+-----------------------------------------------------------+

States:
- Loading: Skeleton table rows
- Empty: "ยังไม่มีสินค้า" + [+ Add Product] CTA
- Low Stock Alert (stock ≤ 5): แถว highlight สีเหลือง + badge "Low Stock"
- Out of Stock (stock = 0): แถว "OOS" badge สีแดง
```

---

## Handoff Digest → Role 4: Developer

**Status:** READY

**Critical Items for Next Role:**
- Primary Persona: นิค (Expert user) — ต้องการ checkout เร็ว ไม่ยุ่งยาก
- Screens: 12 screens สำหรับ Must Have features
- Design System: Primary #2563EB, Font: Inter, Component library: TailwindUI

**Critical UX Flows:**
1. Guest Checkout: ไม่บังคับ login — ให้ checkout ได้โดยไม่มี account
2. Cart Persistence: authenticated user cart sync ข้าม devices
3. Payment Optimism: ห้าม double-submit — disable button ทันทีที่กด
4. PromptPay 15-min expiry: countdown timer ชัดเจน + auto-generate new QR

**Empty/Error States ที่สำคัญ:**
- Product Listing: empty state มี suggested products (ไม่ใช่แค่ข้อความ)
- Cart: empty state มี CTA ชัดเจน
- Payment Failed: error ชัดเจน, cart ไม่หาย

**Key Deliverables Created:**
- `templates/03-ux-ui/user-personas.md` ✅
- `templates/03-ux-ui/journey-map.md` ✅
- `templates/03-ux-ui/wireframes.md` ✅
- `templates/03-ux-ui/design-system.md` ✅
