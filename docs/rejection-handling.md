# Iteration & Rejection Handling Guide

**Version:** 1.0 | **Date:** 2026-03-21

---

## ภาพรวม

Pipeline จะ "ราบรื่น" ในกรณี happy path แต่ในการพัฒนาจริง การ reject งานและขอแก้ไขคือเรื่องปกติ
Guide นี้กำหนด protocol ชัดเจนว่าเมื่อไหร่ควรทำอะไร

---

## 1. ประเภทของการ Reject

| ประเภท | นิยาม | ตัวอย่าง |
|--------|-------|---------|
| **Minor Revision** | แก้ < 30% ของ output — เปลี่ยนเฉพาะจุด | ปรับ wording, เพิ่ม 1 API endpoint, แก้ tech stack 1 ชั้น |
| **Major Revision** | แก้ 30-70% ของ output — ต้องคิดใหม่หลายส่วน | เปลี่ยน architecture pattern, เพิ่ม user group ใหม่, ออกแบบ DB ใหม่ |
| **Full Redo** | แก้ > 70% หรือ assumption พื้นฐานผิด | requirement ที่ AI เข้าใจผิดทั้งหมด, เปลี่ยน tech stack ทั้งหมด |
| **Carry Over** | งานใน Sprint ไม่เสร็จทันเวลา | Story ซับซ้อนกว่าที่ estimate |
| **Blocker** | Role ถัดไปรับ output ที่ยังมีปัญหา Critical ไม่ได้ | Code Review พบ Critical, QA Sign-off เป็น NO-GO |

---

## 2. Decision Tree

```
ผู้ใช้ไม่พอใจ output / พบปัญหา
            |
     ปัญหาอยู่ที่ไหน?
    /         |          \
เฉพาะจุด   หลายจุด   ทั้งหมด
(Minor)    (Major)   (Full Redo)
    |          |          |
ใช้ Targeted  ใช้ Major   ใช้ Full
Fix Prompt   Revision    Redo Prompt
             Prompt
```

### Minor Revision — Targeted Fix

```
แก้เฉพาะส่วนนี้ใน [ชื่อไฟล์]:
- [Section/Item ที่ต้องแก้]: [คำอธิบายที่ต้องการ]
- ส่วนอื่นทั้งหมดให้คงไว้เหมือนเดิม
- อัปเดตไฟล์และ Handoff Digest ให้สอดคล้อง
```

### Major Revision

```
แก้ไข [Role N] output — Major Revision

ส่วนที่ต้องเปลี่ยน:
1. [Section X]: [อธิบายสิ่งที่ต้องการ]
2. [Section Y]: [อธิบายสิ่งที่ต้องการ]

ส่วนที่ให้คงไว้:
- [Section Z]: ดีแล้ว ไม่ต้องเปลี่ยน

หลังแก้เสร็จ อัปเดต:
- [ไฟล์ output หลัก]
- Handoff Digest
- progress-dashboard.md
```

### Full Redo

```
ทำ [Role N] ใหม่ทั้งหมด

เหตุผล: [อธิบาย assumption ที่ผิดหรือสิ่งที่เปลี่ยนไป]

Context ใหม่:
- [ข้อมูลที่ถูกต้อง]
- [constraint ใหม่]

ทำตาม Chain-of-Thought ของ Role [N] ตั้งแต่ต้น
```

---

## 3. Rejection ที่ Checkpoint แต่ละจุด

### Checkpoint 1 (หลัง Phase 1)

| สถานการณ์ | Action |
|-----------|--------|
| ต้องการเพิ่ม/ลด features | Targeted fix ที่ R1 requirements-document.md + user-story-map.md → R2/R11/R3 อัปเดต output ที่เกี่ยวข้อง |
| เปลี่ยน tech stack | Targeted fix ที่ R2 tech-stack.md + api-spec.md → R11 อาจต้องอัปเดต db-schema.md |
| ไม่พอใจ UX/UI | Targeted fix ที่ R3 wireframes.md / design-system.md |
| Sprint Plan ไม่เหมาะ | แก้ sprint plan ใน checkpoint summary โดยตรง ไม่ต้อง redo Role ใด |

### Sprint Review (หลังแต่ละ Sprint)

| สถานการณ์ | Action |
|-----------|--------|
| Story ไม่ครบ AC | R4 ต้อง fix แล้ว R5 review ใหม่ (ไม่ถือว่า sprint เสร็จจนกว่า AC ผ่าน) |
| Code Review: REQUEST CHANGES | ดู Section 4 ด้านล่าง |
| Security: Critical/High | ดู Section 5 ด้านล่าง |
| Carry over story | บันทึกเหตุผล → ย้ายไป Sprint ถัดไปอัตโนมัติ |

### Checkpoint 2 (หลัง Phase 2)

| สถานการณ์ | Action |
|-----------|--------|
| Story สำคัญยังไม่เสร็จ | เปิด Sprint เพิ่ม (Sprint N+1) สำหรับ carry over stories |
| Coverage < 80% | R4 fix tests → R5 review coverage ใหม่ |
| Security ยังมี High open | R6 ระบุ items → R4 fix → R6 verify ใหม่ |

### Checkpoint 3 (หลัง Phase 3)

| สถานการณ์ | Action |
|-----------|--------|
| QA NO-GO | ดู Section 6 ด้านล่าง |
| Documentation ไม่ครบ | R9 targeted fix เฉพาะ section ที่ขาด |

---

## 4. Code Review Iteration Loop

```
R4 Output → R5 Review → [APPROVED?]
                              |
                         Yes: ไป R6
                              |
                         No (REQUEST CHANGES):
                              ↓
                         R5 ระบุ issues ด้วย location + severity + suggestion
                              ↓
                    Critical issues? ──── Yes ──→ R4 must fix ก่อน proceed
                              |
                             No (Warning/Suggestion only)
                              ↓
                    R4 fixes → R5 re-reviews changed files เท่านั้น
                              ↓
                         [APPROVED] → ไป R6
```

**ข้อบังคับ:**
- R5 พบ Critical → R4 ต้องแก้ก่อนเสมอ
- R5 re-review: อ่านเฉพาะไฟล์ที่แก้ ไม่ต้อง review ทุกไฟล์ใหม่
- ถ้า R4 แก้แล้วยัง fail 2 รอบ → flag ให้ผู้ใช้ตัดสินใจ

---

## 5. Security Issue Remediation Loop

```
R6 Security Scan → [PASSED?]
                        |
                   Yes: ไป QA
                        |
                   No (Critical/High found):
                        ↓
              R6 ระบุ: vulnerability + remediation code snippet
                        ↓
              ซับซ้อนเกิน AI ทำเองได้? ──── Yes ──→ flag ให้ human
                        |
                       No
                        ↓
              R4 apply remediation → R6 re-scan affected components
                        ↓
                  [PASSED] → ไป QA
```

**ข้อบังคับ:**
- Critical security ห้ามผ่านไป QA ก่อน fix
- High security ควร fix ก่อน แต่ถ้า mitigated บาง Sprint ได้ถ้า log ไว้ใน remediation-plan.md
- R6 re-scan: focus ที่ affected files เท่านั้น

---

## 6. QA NO-GO Loop

```
R7 QA → Sign-off: [GO / NO-GO]
                        |
                   GO: ไป R8 DevOps
                        |
                   NO-GO (P0/P1 bugs open):
                        ↓
              R7 Bug Report ชัดเจน: steps to reproduce + expected/actual + severity
                        ↓
              R4 fixes bugs → R7 re-runs affected test cases
                        ↓
              [All P0/P1 resolved] → GO → R8
```

**ข้อบังคับ:**
- R8 DevOps ห้าม proceed ถ้า Sign-off ยังเป็น NO-GO
- P0 (Critical) bugs ต้องแก้ก่อน 100%
- P1 (High) bugs ต้องแก้ก่อน หรือมี accepted workaround ที่ documented

---

## 7. Architecture Review Gate (R6 Phase 1)

```
R6 Phase 1 Architecture Review → [APPROVED / ISSUES FOUND]
                                          |
                                    APPROVED:
                                    ไป R3 UX/UI
                                          |
                                    ISSUES FOUND (Critical/High):
                                          ↓
                              R6 ระบุ specific gaps + recommendations
                                          ↓
                              R2 แก้ architecture-diagram.md + api-spec.md
                                          ↓
                              R6 ตรวจใหม่เฉพาะจุดที่แก้
                                          ↓
                                    [APPROVED] → ไป R3
```

---

## 8. Revision Request Template

ใช้ template นี้เพื่อบอก AI ว่าต้องการแก้อะไร:

```markdown
## Revision Request — [Role N] [ชื่อไฟล์]

**ประเภท:** Minor / Major / Full Redo
**เหตุผล:** [อธิบายว่าทำไมต้องแก้]

**สิ่งที่ต้องแก้:**
1. [Section/Item]: [ต้องการอะไร]
2. [Section/Item]: [ต้องการอะไร]

**สิ่งที่คงไว้:**
- [ส่วนที่พอใจแล้ว]

**Downstream Impact:**
- ถ้าแก้จุดนี้ → [ไฟล์ Role อื่นที่ต้องอัปเดตด้วย]
```

---

## 9. Downstream Impact Matrix

เมื่อแก้ไขไฟล์หนึ่ง ต้องตรวจว่า Role อื่นต้องอัปเดตด้วยไหม:

| ถ้าแก้ไฟล์นี้... | ต้องตรวจ / อัปเดต... |
|-----------------|---------------------|
| requirements-document.md | user-story-map.md, risk-analysis.md, sprint plan |
| tech-stack.md | api-spec.md, db-schema.md, code ที่ใช้ tech นั้น |
| api-spec.md | โค้ด controller, test cases, api-docs.md |
| db-schema.md | migrations, repository layer, R7 test data |
| wireframes.md | Frontend code, design-system.md |
| security-policies.md | โค้ด auth middleware, cicd-pipeline.md |
| progress-dashboard.md | (ไม่มี downstream — มันคือ state file) |

---

## 10. Max Iteration Rule

เพื่อป้องกัน infinite loop:

| Scenario | Max Rounds | Escalation |
|----------|-----------|------------|
| Code Review iteration | 3 rounds | Flag ให้ human ตัดสินใจว่าจะ proceed ยังไง |
| Security remediation | 2 rounds | Flag items ที่ยังไม่ resolved ใน security-report.md |
| QA bug fix | 2 rounds | Mark P1 bugs เป็น "Accepted Risk" ถ้า mitigated |
| Architecture review | 2 rounds | Human decides: proceed with known risks หรือ redesign |
