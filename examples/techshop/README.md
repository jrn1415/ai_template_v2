# TechShop E-commerce — Example Project Outputs

> ตัวอย่าง output จริงจากการใช้ AI Template v2 กับโปรเจกต์ TechShop E-commerce

---

## โปรเจกต์นี้คืออะไร

**TechShop** คือร้านขายอุปกรณ์ IT/Electronics ออนไลน์ ที่รับชำระผ่าน Stripe + PromptPay
ใช้เป็น reference project ตลอดทั้ง template (ปรากฏใน few-shot examples ของทุก Role)

**Stack:** React + .NET 10 + PostgreSQL | **Scale:** Medium (5,000 MAU)

---

## ไฟล์ตัวอย่างในแต่ละ Role

| Role | ไฟล์ตัวอย่าง | สิ่งที่แสดง |
|------|------------|------------|
| R1 — Requirements | [01-requirements/requirements-document.md](01-requirements/requirements-document.md) | Functional Requirements, NFRs, User Stories, MoSCoW |
| R2 — Architecture | [02-architecture/architecture-diagram.md](02-architecture/architecture-diagram.md) | System diagram, ADR, component breakdown |
| R11 — DBA | [11-dba/db-schema.md](11-dba/db-schema.md) | ER Diagram, Table Definitions, Indexing, Security |
| R3 — UX/UI | [03-ux-ui/wireframes.md](03-ux-ui/wireframes.md) | Wireframes ทุก state, Screen Inventory |
| R4 — Developer | [04-development/code-structure.md](04-development/code-structure.md) | Project structure, Sprint 1 code summary |
| R5 — Code Review | [05-code-review/review-report.md](05-code-review/review-report.md) | Review report Sprint 1 พร้อม Checklist |
| R6 — Security | [06-security/security-report.md](06-security/security-report.md) | OWASP Assessment, findings, remediation |
| R7 — QA | [07-qa-testing/test-cases.md](07-qa-testing/test-cases.md) | Test cases สำหรับ Sprint 1 stories |
| R8 — DevOps | [08-devops/cicd-pipeline.md](08-devops/cicd-pipeline.md) | CI/CD pipeline design |
| R9 — Documentation | [09-documentation/user-manual.md](09-documentation/user-manual.md) | User manual (Getting Started) |
| R10 — PM | [10-project-management/progress-dashboard.md](10-project-management/progress-dashboard.md) | Completed progress dashboard |

---

## วิธีใช้ตัวอย่างเหล่านี้

1. **เป็น quality benchmark** — เปรียบ output ที่ AI สร้างให้กับ output ในโฟลเดอร์นี้
2. **เป็น format reference** — ดูว่า section แต่ละส่วนควรเขียนอย่างไร
3. **ไม่ควร copy-paste** — ตัวอย่างเหล่านี้เป็นของ TechShop, โปรเจกต์ของคุณต่างออกไป

---

## ข้อมูลโปรเจกต์ TechShop

```
ชื่อระบบ: TechShop Online Store
Business Goal: สร้างช่องทางขายอุปกรณ์ IT online พร้อมระบบ inventory + order management
กลุ่มผู้ใช้: ลูกค้าทั่วไป (B2C) + Admin
Must Have Features:
  - Product catalog with search & filter
  - Shopping cart
  - Checkout (Stripe + PromptPay)
  - Order tracking
  - Admin: product + order management
Tech Stack: React 19 + .NET 10 (ASP.NET Core) + PostgreSQL 16
Scale: 5,000 MAU, 500 concurrent users peak
```
