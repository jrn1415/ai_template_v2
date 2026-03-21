# Context Window & Memory Management Guide

**Version:** 1.0 | **Date:** 2026-03-21

---

## ปัญหาที่แก้

Auto-Pipeline มีทั้งหมด 11 Role และหลาย Sprint ทำให้ context window ของ AI เต็มได้ก่อนที่งานจะเสร็จ
Guide นี้อธิบาย:
1. วิธีสังเกตว่า context ใกล้เต็ม
2. วิธีแบ่งงานเพื่อจัดการ context
3. วิธี resume pipeline ในเซสชันใหม่

---

## 1. Context Budget ประมาณการ

| Phase / Role | Context ที่ใช้ (ประมาณ) | กลยุทธ์ |
|---|---|---|
| Phase 1 (R1–R3 + R6) | ~50,000 tokens | รันใน session เดียวได้สบาย |
| Sprint 1 (R4+R5+R6) | ~80,000 tokens | ควรรันใน session ใหม่หลัง Phase 1 |
| Sprint N (R4+R5+R6) | ~60,000 tokens per sprint | 1 session ต่อ 1 Sprint |
| Phase 3 (R7+R8+R9) | ~60,000 tokens | 1 session |
| Phase 4 (R10) | ~20,000 tokens | 1 session |

> **กฎ:** ถ้า context เริ่มหนัก หรือ AI เริ่มลืม context เก่า → เริ่ม session ใหม่ แล้วใช้ Resume Protocol

---

## 2. สัญญาณว่า Context ใกล้เต็ม

- AI ตอบโดยไม่อ้างอิงข้อมูลจาก Role ก่อนหน้า (เช่น ลืม Tech Stack ที่เลือกไว้)
- AI ถามข้อมูลที่เคยให้ไปแล้ว
- Response ช้าลง หรือ ถูกตัดกลางทาง
- AI ทำซ้ำงานที่ทำไปแล้ว
- เกิด error "context length exceeded"

---

## 3. Session Resume Protocol

เมื่อต้องการ resume pipeline ในเซสชันใหม่ ให้ส่ง prompt นี้ให้ AI:

```
Resume Pipeline — [ชื่อโปรเจกต์]

อ่านไฟล์ต่อไปนี้เพื่อ restore context ก่อนทำงาน:

READ: templates/10-project-management/progress-dashboard.md
READ: templates/01-requirements/requirements-document.md
READ: templates/02-architecture/tech-stack.md
READ: templates/02-architecture/api-spec.md
```

จาก progress-dashboard.md ให้:
1. ดู Current Sprint และสถานะล่าสุด
2. ดู Handoff Digest ของ Role ล่าสุดที่เสร็จ
3. ดู Open Issues & Blockers
4. แล้วต่องานจาก Role / Sprint ที่ยังค้างอยู่

```

### Role ที่กำลังเริ่มต้น Sprint ใหม่

```
Resume Pipeline — Sprint [N]

READ: templates/10-project-management/progress-dashboard.md
READ: templates/01-requirements/user-story-map.md
READ: templates/02-architecture/tech-stack.md
READ: templates/02-architecture/api-spec.md
READ: templates/11-dba/db-schema.md
READ: templates/03-ux-ui/wireframes.md

เริ่ม Sprint [N]: [ชื่อ Sprint]
Stories ใน Sprint นี้: [US-XXX], [US-XXX]
```

---

## 4. Chunking Strategy — แบ่งงานอย่างไร

### Option A: Phase-based Sessions (แนะนำ)

```
Session 1: Phase 1 (R1 → R2 → R11 → R6-review → R3) + Checkpoint 1
Session 2: Sprint 1 (R4 → R5 → R6)
Session 3: Sprint 2 (R4 → R5 → R6)
Session N: Sprint N (R4 → R5 → R6)
Session N+1: Phase 3 (R7 → R8 → R9) + Checkpoint 3
Session N+2: Phase 4 (R10)
```

### Option B: Role-based Sessions (โปรเจกต์ซับซ้อนมาก)

ถ้าแต่ละ Role มี output ยาวมาก ให้แบ่ง 1 Role ต่อ 1 Session:

```
Session 1: R1 (Requirements)
Session 2: R2 (Architecture) + R11 (DBA) + R6 Phase 1
Session 3: R3 (UX/UI)
Session 4+: Sprint-based
```

---

## 5. Handoff Digest เป็น Context Anchor

ทุก Role มี **Handoff Digest** ที่เขียนไว้ในไฟล์ output เช่น:
- Role 1 → เขียน Handoff ท้าย `requirements-document.md`
- Role 2 → เขียน Handoff ท้าย `tech-stack.md`
- Role 4 → เขียน Handoff ใน `progress-dashboard.md` (Sprint section)

เมื่อ resume ใน session ใหม่ **อ่าน Handoff Digest ก่อนเสมอ** เพราะมันสรุป:
- Status (READY / BLOCKED)
- Critical Items ที่ Role ถัดไปต้องรู้
- Open Decisions ที่ยังค้าง
- Key Deliverables ที่สร้างไว้

---

## 6. Progress Dashboard คือ "State File"

`templates/10-project-management/progress-dashboard.md` คือไฟล์เดียวที่บอก
ทุกอย่างเกี่ยวกับ pipeline ณ ขณะนั้น:

| ข้อมูล | หาได้ที่ |
|--------|---------|
| Role ใดเสร็จแล้ว | Role Completion table |
| Sprint ไหนกำลังทำ | Sprint Progress table |
| มี Blocker อะไร | Issues & Blockers section |
| ไฟล์อะไรถูกสร้าง | Deliverables Registry |
| ตัดสินใจอะไรไว้บ้าง | Key Decisions log |
| Activity ล่าสุด | Activity Log |

**กฎ:** เมื่อเริ่ม session ใหม่ อ่าน `progress-dashboard.md` เป็นไฟล์แรกเสมอ

---

## 7. ตัวอย่าง Resume ในทางปฏิบัติ

### สถานการณ์: Phase 1 เสร็จ ต้องการเริ่ม Sprint 1

Session ใหม่ — ส่ง prompt:

```
Resume Pipeline — TechShop

อ่านไฟล์ context:
- templates/10-project-management/progress-dashboard.md
- templates/01-requirements/user-story-map.md (ดู Sprint 1 stories)
- templates/02-architecture/tech-stack.md
- templates/02-architecture/api-spec.md
- templates/11-dba/db-schema.md
- templates/03-ux-ui/wireframes.md
- templates/03-ux-ui/design-system.md

Phase 1 เสร็จแล้ว Sprint Plan approved
เริ่ม Sprint 1: "Foundation & Auth"
Stories: US-001 (User Registration), US-002 (User Login), US-003 (Product Catalog)
```

### สถานการณ์: กลาง Sprint 2 context เต็ม

Session ใหม่ — ส่ง prompt:

```
Resume Pipeline — TechShop Sprint 2

อ่านไฟล์ context:
- templates/10-project-management/progress-dashboard.md  ← ดู Sprint 2 status
- templates/04-development/code-structure.md             ← ดูโครงสร้างโค้ดที่ทำไว้

Sprint 2 "Cart & Checkout" ยังค้างอยู่
US-005 (Add to Cart) เสร็จแล้ว
กำลังทำ US-006 (Checkout Flow) — ยังไม่เสร็จ
ต้องการต่องาน US-006
```

---

## 8. Best Practices สรุป

| Do | Don't |
|----|-------|
| เริ่ม session ใหม่ทุก Sprint | พยายามทำ 3+ Sprint ใน session เดียว |
| อ่าน progress-dashboard.md ก่อนเสมอ | เริ่มทำงานโดยไม่ restore context |
| ใช้ Handoff Digest เป็น context anchor | อ่านไฟล์ทั้งหมดทุกครั้ง (สิ้นเปลือง) |
| บันทึก state ลง progress-dashboard.md ระหว่าง Sprint | พึ่งความจำของ AI เก็บ state |
| แบ่งโปรเจกต์ใหญ่เป็น session ย่อยๆ | ยัด context ทั้งหมดใน session เดียว |
