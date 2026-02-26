# วิธีการใช้งาน Template

## คู่มือเริ่มต้นใช้งานฉบับเร็ว

---

## ขั้นตอนที่ 1: ตั้งค่าโครงการของคุณ

1. Clone หรือ copy template repository นี้มาใช้งาน
2. เปิดไฟล์ `CLAUDE.md` แล้วกรอกข้อมูลโครงการ:
   - **ชื่อระบบ** (System Name) - เช่น "ระบบจัดการคลังสินค้า"
   - **เป้าหมายธุรกิจ** (Business Goal) - เช่น "ลดเวลาจัดการคลังสินค้า 50%"
   - **ผู้ใช้งานหลัก** (Primary Users) - เช่น "พนักงานคลังสินค้า, ผู้จัดการ"
   - **ข้อจำกัด** (Constraints) - เช่น "ต้องรองรับ 1,000 users พร้อมกัน"

## ขั้นตอนที่ 2: ทำตาม Workflow ตามลำดับ

### ลำดับการทำงาน

```
 1. วิเคราะห์ความต้องการ  →  กรอก templates/requirements/
 2. ออกแบบสถาปัตยกรรม     →  กรอก templates/architecture/
 3. ออกแบบ UX/UI          →  กรอก templates/ux-ui/
 4. พัฒนาระบบ             →  ใช้  templates/development/
 5. ตรวจสอบโค้ด           →  ใช้  templates/code-review/
 6. ตรวจสอบความปลอดภัย    →  ใช้  templates/security/
 7. ทดสอบคุณภาพ           →  ใช้  templates/qa-testing/
 8. จัดการ DevOps          →  ใช้  templates/devops/
 9. เขียนเอกสาร           →  ใช้  templates/documentation/
10. บริหารโครงการ          →  ใช้  templates/project-management/
```

> **หมายเหตุ**: ไม่จำเป็นต้องทำทุกขั้นตอน สามารถเลือกเฉพาะขั้นตอนที่ต้องการได้

---

## ขั้นตอนที่ 3: ใช้งานร่วมกับ AI (Claude / ChatGPT / อื่นๆ)

### วิธี A: จำลองทีมพัฒนาทั้งหมด (แนะนำสำหรับโปรเจกต์ใหม่)

1. Copy prompt จากไฟล์ `.ai-prompts/[role]/prompt.md`
2. วางลงในเครื่องมือ AI ที่ใช้งาน
3. แทนที่ `[placeholders]` ทั้งหมดด้วยข้อมูลจริงของโครงการ
4. AI จะสร้างผลลัพธ์ตาม template ที่กำหนด

**ตัวอย่าง**:
```
1. เปิดไฟล์ .ai-prompts/01-requirements/prompt.md
2. Copy ข้อความทั้งหมด
3. วางใน Claude/ChatGPT
4. แทนที่ [SYSTEM_NAME] เป็น "ระบบจัดการคลังสินค้า"
5. แทนที่ [BUSINESS_GOAL] เป็น "ลดเวลาจัดการคลังสินค้า 50%"
6. ส่งข้อความ แล้ว AI จะสร้าง Requirements Document ให้
```

### วิธี B: ใช้เฉพาะบาง Role (แนะนำสำหรับงานเฉพาะด้าน)

ถ้าต้องการเฉพาะบาง Role (เช่น ต้องการแค่ Code Review) ให้ใช้ prompt ของ Role นั้นโดยตรง

**ตัวอย่างสถานการณ์**:
- มีโค้ดอยู่แล้ว ต้องการ review → ใช้ `05-code-review/prompt.md`
- ต้องการออกแบบ database → ใช้ `02-architecture/prompt.md`
- ต้องการสร้าง test plan → ใช้ `07-qa-testing/prompt.md`

### วิธี C: ทำงานต่อเนื่อง (Sequential Workflow)

1. เริ่มจาก Role 1 (Requirement Analyst) — ได้ Requirements Document
2. นำผลลัพธ์จาก Role 1 ป้อนเข้า Role 2 (System Architect) — ได้ Architecture
3. นำผลลัพธ์จาก Role 2 ป้อนเข้า Role 3 (UX/UI Designer) — ได้ UI Design
4. ทำต่อเนื่องไปจนครบ pipeline

> **เคล็ดลับ**: ผลลัพธ์จากแต่ละ Role จะเป็น input ให้กับ Role ถัดไป
> ยิ่งให้ข้อมูลละเอียดมากเท่าไหร่ ผลลัพธ์ก็จะยิ่งดีมากขึ้น

---

## ขั้นตอนที่ 4: ปรับแต่งตามความต้องการ

- แก้ไข template ให้ตรงกับความต้องการเฉพาะของทีม
- เพิ่มหรือลด Role ตามขนาดโครงการ
- ปรับเกณฑ์ Definition of Done ตามมาตรฐานองค์กร
- อัปเดตรายละเอียดเทคโนโลยีที่ใช้จริง

---

## เคล็ดลับการใช้งาน

| เคล็ดลับ | รายละเอียด |
|---------|-----------|
| เริ่มจาก Requirements | ใช้ prompt **Requirement Analyst** เพื่อกำหนดขอบเขตโครงการก่อนเสมอ |
| ลงทุนกับ Architecture | ขั้นตอน **Architecture** สำคัญมาก ควรใช้เวลากับส่วนนี้ให้เพียงพอ |
| อย่าข้าม Security | ต้อง review **Security** ก่อน deploy ทุกครั้ง |
| เอกสารทำตลอด | อัปเดต **Documentation** ไปพร้อมกับการพัฒนา อย่ารอทำตอนท้าย |
| สื่อสารกับ Stakeholders | ใช้ **PM templates** สำหรับรายงานความคืบหน้า |
| ใช้ MoSCoW | จัดลำดับความสำคัญด้วย Must/Should/Could/Won't เสมอ |
| ทำ MVP ก่อน | เลือกเฉพาะ "Must have" สำหรับ release แรก |

---

## รูปแบบการใช้งาน

| รูปแบบ | เหมาะสำหรับ | วิธีใช้ |
|--------|------------|--------|
| **Full Simulation** | โปรเจกต์ใหม่ตั้งแต่เริ่มต้น | ใช้ทุก Role ตามลำดับ 1→10 |
| **Single Role** | งานเฉพาะด้าน | เลือกใช้เฉพาะ Role ที่ต้องการ |
| **Template Only** | ทีมมีคนจริงแล้ว | ใช้เฉพาะ template เป็นโครงสร้างเอกสาร |
| **Hybrid** | ทีมเล็ก + AI ช่วย | ให้คนทำบาง Role + AI ทำบาง Role |

---

## ตัวอย่างสถานการณ์จริง

### สถานการณ์ 1: สร้างระบบใหม่ตั้งแต่ศูนย์

```
1. กรอกข้อมูลใน CLAUDE.md
2. ใช้ Role 1 (Requirements) → ได้ User Stories + Priority Matrix
3. ใช้ Role 2 (Architecture) → ได้ Architecture + Tech Stack + API Spec
4. ใช้ Role 3 (UX/UI) → ได้ Design System + Wireframes
5. เริ่มพัฒนาตาม Role 4 (Development)
6. ตรวจสอบด้วย Role 5-7 (Review + Security + QA)
7. Deploy ด้วย Role 8 (DevOps)
8. สร้างเอกสารด้วย Role 9 (Documentation)
```

### สถานการณ์ 2: มีระบบอยู่แล้ว ต้องการเพิ่มฟีเจอร์

```
1. ใช้ Role 1 (Requirements) → เขียน User Stories เฉพาะฟีเจอร์ใหม่
2. ใช้ Role 2 (Architecture) → ออกแบบส่วนที่ต้องแก้ไข
3. พัฒนาตาม Role 4 (Development)
4. ตรวจสอบด้วย Role 5 (Code Review)
5. ทดสอบด้วย Role 7 (QA)
```

### สถานการณ์ 3: ต้องการ Review โค้ดที่มีอยู่

```
1. ใช้ Role 5 (Code Review) → ตรวจสอบคุณภาพโค้ด
2. ใช้ Role 6 (Security) → ตรวจสอบความปลอดภัย
3. แก้ไขตาม feedback
```

---

## โครงสร้างไฟล์ทั้งหมด

```
.
├── CLAUDE.md                          # ไฟล์ตั้งค่าหลักของโครงการ
├── .ai-prompts/                       # Prompt สำหรับ AI แต่ละ Role
│   ├── 01-requirements/prompt.md      #   นักวิเคราะห์ความต้องการ
│   ├── 02-architecture/prompt.md      #   สถาปนิกระบบ
│   ├── 03-ux-ui/prompt.md             #   นักออกแบบ UX/UI
│   ├── 04-development/prompt.md       #   นักพัฒนา
│   ├── 05-code-review/prompt.md       #   ผู้ตรวจสอบโค้ด
│   ├── 06-security/prompt.md          #   วิศวกรความปลอดภัย
│   ├── 07-qa-testing/prompt.md        #   นักทดสอบคุณภาพ
│   ├── 08-devops/prompt.md            #   วิศวกร DevOps
│   ├── 09-documentation/prompt.md     #   นักเขียนเอกสาร
│   └── 10-project-management/prompt.md #  Product Owner / PM
│
├── templates/                         # Template สำหรับเอกสารส่งมอบ
│   ├── requirements/                  #   เอกสารความต้องการ (4 ไฟล์)
│   ├── architecture/                  #   เอกสารสถาปัตยกรรม (5 ไฟล์)
│   ├── ux-ui/                         #   เอกสารออกแบบ UI (5 ไฟล์)
│   ├── development/                   #   เอกสารพัฒนา (3 ไฟล์)
│   ├── code-review/                   #   เอกสารตรวจสอบโค้ด (2 ไฟล์)
│   ├── security/                      #   เอกสารความปลอดภัย (5 ไฟล์)
│   ├── qa-testing/                    #   เอกสารทดสอบ (5 ไฟล์)
│   ├── devops/                        #   เอกสาร DevOps (6 ไฟล์)
│   ├── documentation/                 #   เอกสารสำหรับผู้ใช้ (6 ไฟล์)
│   └── project-management/            #   เอกสารบริหารโครงการ (5 ไฟล์)
│
├── docs/
│   ├── workflow.md                    # ผังกระบวนการ SDLC
│   ├── how-to-use-en.md              # คู่มือภาษาอังกฤษ
│   └── how-to-use-th.md              # ไฟล์นี้ (ภาษาไทย)
│
└── README.md                          # ภาพรวมโครงการ
```

---

## คำถามที่พบบ่อย (FAQ)

### Q: ต้องใช้ทุก Role ไหม?
**A**: ไม่จำเป็น เลือกเฉพาะ Role ที่ต้องการได้ แต่แนะนำอย่างน้อย: Requirements → Architecture → Development → Code Review → QA

### Q: ใช้กับ AI ตัวไหนได้บ้าง?
**A**: ใช้ได้กับ AI ทุกตัวที่รองรับ text input เช่น Claude, ChatGPT, Gemini, Copilot ฯลฯ

### Q: ต้องทำตามลำดับเป๊ะไหม?
**A**: ควรทำตามลำดับ เพราะผลลัพธ์ของ Role ก่อนหน้าจะเป็น input ของ Role ถัดไป แต่ถ้าเป็นงานเฉพาะด้านก็ข้ามได้

### Q: Template ปรับแต่งได้ไหม?
**A**: ได้ ทุก template ออกแบบมาให้ปรับแต่งได้ตามความต้องการของทีมและโครงการ

### Q: เหมาะกับโครงการขนาดไหน?
**A**: ใช้ได้ตั้งแต่โครงการเล็ก (เลือกแค่ 3-4 Role) ไปจนถึงโครงการใหญ่ (ใช้ทุก Role)
