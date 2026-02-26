# AI Code Template - จำลองทีมพัฒนาซอฟต์แวร์

Template กลางสำหรับจำลองทีมพัฒนาซอฟต์แวร์ครบวงจร 10 บทบาท ออกแบบมาให้ใช้งานร่วมกับ AI Coding Assistants (Claude, ChatGPT ฯลฯ) หรือใช้เป็น SDLC Framework แบบ standalone ก็ได้

## สิ่งที่มีอยู่ใน Template

### AI Prompts (`.ai-prompts/`)

| # | บทบาท | หน้าที่ |
|---|-------|--------|
| 01 | นักวิเคราะห์ความต้องการ (Requirement Analyst) | รวบรวมและจัดลำดับความต้องการ, สร้าง User Stories |
| 02 | สถาปนิกระบบ (System Architect) | ออกแบบสถาปัตยกรรม, เลือก Tech Stack, กำหนด API |
| 03 | นักออกแบบ UX/UI (UX/UI Designer) | สร้าง Personas, Wireframes, Design System |
| 04 | นักพัฒนา (Software Developer) | เขียนโค้ดตามมาตรฐาน, ทดสอบ, เอกสาร |
| 05 | ผู้ตรวจสอบโค้ด (Code Reviewer) | ตรวจสอบคุณภาพโค้ด, ความปลอดภัย, ประสิทธิภาพ |
| 06 | วิศวกรความปลอดภัย (Security Engineer) | Threat Modeling, ประเมิน OWASP, นโยบายความปลอดภัย |
| 07 | นักทดสอบคุณภาพ (QA/Tester) | วางแผนทดสอบ, ดำเนินการทดสอบ, รายงาน Bug |
| 08 | วิศวกร DevOps (DevOps/CICD) | สร้าง CI/CD Pipeline, จัดการ Infrastructure, Monitoring |
| 09 | นักเขียนเอกสาร (Technical Writer) | คู่มือผู้ใช้, เอกสาร API, คู่มือ Onboarding |
| 10 | Product Owner/PM | วางแผน Sprint, ติดตามงาน, สื่อสารกับ Stakeholders |

### Template สำหรับเอกสารส่งมอบ (`templates/`)

50+ template พร้อมใช้งาน ครอบคลุมทุกขั้นตอนของการพัฒนาซอฟต์แวร์:

- **วิเคราะห์ความต้องการ**: เอกสารความต้องการ, User Story Map, Priority Matrix, วิเคราะห์ความเสี่ยง
- **สถาปัตยกรรม**: Architecture Diagram, Tech Stack, API Spec, DB Schema, Data Flow
- **ออกแบบ UX/UI**: User Personas, Journey Map, Wireframes, Design System, Usability Testing
- **พัฒนา**: README Template, มาตรฐานการทดสอบ, PR Template
- **ตรวจสอบโค้ด**: รายงาน Code Review, Checklist การตรวจสอบ
- **ความปลอดภัย**: Threat Model (STRIDE), ประเมิน OWASP, รายงานความปลอดภัย, แผนแก้ไข, นโยบาย
- **ทดสอบคุณภาพ**: Test Plan, Test Cases, Bug Report, Performance Test, QA Sign-off
- **DevOps**: CI/CD Pipeline, Docker Config, Monitoring, Runbooks, Environments, Infrastructure
- **เอกสาร**: คู่มือผู้ใช้, เอกสาร API, Onboarding, Troubleshooting, Release Notes, ADR
- **บริหารโครงการ**: Roadmap, Sprint Plan, Status Report, Risk Register, Meeting Templates, **Progress Dashboard**

## เริ่มต้นใช้งาน

### Auto-Pipeline (แนะนำ — ง่ายที่สุด)

1. กรอกข้อมูลโครงการในไฟล์ `requirement_template.md`
2. สั่ง Claude: `"เริ่มพัฒนาตาม auto-pipeline จาก requirement_template.md"`
3. Claude จะดำเนินการทุก Role อัตโนมัติ พัฒนาแบบ Sprint-based พร้อม Checkpoint ให้ review ทุก Phase

```
กรอก requirement_template.md
        ↓
AI ตรวจสอบ + ถามเพิ่ม (ถ้าจำเป็น)
        ↓
Phase 1: Requirements → Architecture → UX/UI → Sprint Planning
        ↓ ⏸️ Checkpoint 1 (review + ตรวจ Sprint Plan)
Phase 2: พัฒนาแบบ Sprint-based (ทำทีละ Sprint)
        ├─ Sprint N: Development → Code Review → Security
        ↓ ⏸️ Sprint Review (ตรวจผลงานแต่ละ Sprint)
        └─ วนจนครบทุก Sprint
        ↓ ⏸️ Checkpoint 2 (review ภาพรวม)
Phase 3: QA Testing → DevOps → Documentation         ⏸️ Checkpoint 3
Phase 4: Project Summary → ส่งมอบทั้งหมด (พร้อมสรุปราย Sprint)
```

### Manual Mode (เลือกทำทีละ Role)

1. กรอกข้อมูลโครงการในไฟล์ `CLAUDE.md`
2. Copy AI prompt จาก `.ai-prompts/[role]/prompt.md`
3. แทนที่ `[placeholders]` ด้วยข้อมูลจริงของโครงการ
4. ใช้ template จาก `templates/` เป็นโครงสร้างผลลัพธ์
5. ทำตาม workflow ที่กำหนดใน `docs/workflow.md`

> **อ่านคู่มือฉบับเต็ม**: [`docs/how-to-use-th.md`](docs/how-to-use-th.md)

## ผังกระบวนการทำงาน (Workflow)

```
วิเคราะห์ความต้องการ --> ออกแบบสถาปัตยกรรม --> ออกแบบ UX/UI --> วางแผน Sprint
                              |                                      |
                              |                               พัฒนาแบบ Sprint-based
                              |                               ├─ Sprint N: พัฒนา → ตรวจสอบโค้ด
                       ตรวจสอบความปลอดภัย                      └─ Sprint Review ทุก Sprint
                              |                                      |
                         ทดสอบคุณภาพ <------------- Security Scan
                              |
                        DevOps Deploy --> Production
                              |
                    เขียนเอกสาร (ทำตลอดกระบวนการ)
                    Product Owner (ประสานงานทุกฝ่าย)
```

## โครงสร้างไฟล์

```
.
├── CLAUDE.md                    # ไฟล์ตั้งค่าหลักของโครงการ
├── requirement_template.md      # แบบฟอร์มกรอกข้อมูลโครงการ (ใช้กับ Auto-Pipeline)
├── .ai-prompts/                 # AI Prompt 10 บทบาท + Auto-Pipeline
│   ├── auto-pipeline-prompt.md  #   Master prompt (สั่ง run ทุก Role อัตโนมัติ)
│   ├── 01-requirements/         #   นักวิเคราะห์ความต้องการ
│   ├── 02-architecture/         #   สถาปนิกระบบ
│   ├── 03-ux-ui/                #   นักออกแบบ UX/UI
│   ├── 04-development/          #   นักพัฒนา
│   ├── 05-code-review/          #   ผู้ตรวจสอบโค้ด
│   ├── 06-security/             #   วิศวกรความปลอดภัย
│   ├── 07-qa-testing/           #   นักทดสอบคุณภาพ
│   ├── 08-devops/               #   วิศวกร DevOps
│   ├── 09-documentation/        #   นักเขียนเอกสาร
│   └── 10-project-management/   #   Product Owner / PM
├── templates/                   # Template เอกสารส่งมอบ 50+ ไฟล์
│   ├── requirements/            #   เอกสารความต้องการ (4 ไฟล์)
│   ├── architecture/            #   เอกสารสถาปัตยกรรม (5 ไฟล์)
│   ├── ux-ui/                   #   เอกสารออกแบบ UI (5 ไฟล์)
│   ├── development/             #   เอกสารพัฒนา (3 ไฟล์)
│   ├── code-review/             #   เอกสารตรวจสอบโค้ด (2 ไฟล์)
│   ├── security/                #   เอกสารความปลอดภัย (5 ไฟล์)
│   ├── qa-testing/              #   เอกสารทดสอบ (5 ไฟล์)
│   ├── devops/                  #   เอกสาร DevOps (6 ไฟล์)
│   ├── documentation/           #   เอกสารสำหรับผู้ใช้ (6 ไฟล์)
│   └── project-management/      #   เอกสารบริหารโครงการ (6 ไฟล์)
├── docs/
│   ├── workflow.md              # ผังกระบวนการ SDLC
│   ├── how-to-use-en.md         # คู่มือการใช้งาน (อังกฤษ)
│   └── how-to-use-th.md         # คู่มือการใช้งาน (ไทย)
├── README.md                    # ภาพรวมโครงการ (อังกฤษ)
└── README-th.md                 # ภาพรวมโครงการ (ไทย) — ไฟล์นี้
```

## รูปแบบการใช้งาน

| รูปแบบ | คำอธิบาย |
|--------|---------|
| **Auto-Pipeline** | กรอก requirement template → AI ทำทุก Role อัตโนมัติ พัฒนาแบบ Sprint-based พร้อม Checkpoint |
| **Full Simulation** | ใช้ทั้ง 10 บทบาทตามลำดับ ควบคุมเองทุกขั้นตอน |
| **Single Role** | เลือกใช้เฉพาะบทบาทที่ต้องการ สำหรับงานเฉพาะด้าน |
| **Template Only** | ใช้เฉพาะ template เป็นโครงสร้างเอกสาร ไม่ต้องใช้ AI prompt |
| **Hybrid** | ผสมผสาน AI prompt กับกระบวนการทำงานจริงของทีม |

## เอกสารที่เกี่ยวข้อง

| เอกสาร | คำอธิบาย |
|--------|---------|
| [`requirement_template.md`](requirement_template.md) | แบบฟอร์มกรอกข้อมูลโครงการ — **เริ่มที่นี่** |
| [`CLAUDE.md`](CLAUDE.md) | ไฟล์ตั้งค่าหลัก + วิธีใช้งาน Auto-Pipeline |
| [`docs/how-to-use-th.md`](docs/how-to-use-th.md) | คู่มือการใช้งานฉบับเต็ม (ภาษาไทย) |
| [`docs/how-to-use-en.md`](docs/how-to-use-en.md) | คู่มือการใช้งานฉบับเต็ม (English) |
| [`docs/workflow.md`](docs/workflow.md) | ผังกระบวนการ SDLC และ Definition of Done |
