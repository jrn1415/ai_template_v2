# CLAUDE.md - Software Development Team Template

## Project Information

- **System Name**: [SYSTEM_NAME]
- **Business Goal**: [BUSINESS_GOAL]
- **Primary Users**: [PRIMARY_USERS]
- **Constraints/Special Conditions**: [CONSTRAINTS]

---

## วิธีใช้งาน (How to Use)

### Mode 1: Auto-Pipeline (แนะนำ — ง่ายที่สุด)

ระบบจะทำงานทุก Role อัตโนมัติ แค่กรอก requirement แล้วสั่งเริ่ม

**ขั้นตอน:**

1. กรอกข้อมูลโครงการในไฟล์ `requirement_template.md`
2. สั่ง Claude:

```
เริ่มพัฒนาตาม auto-pipeline จาก requirement_template.md
```

3. Claude จะ:
   - ตรวจสอบว่าข้อมูลครบไหม (ถ้าไม่ครบจะถามเพิ่ม)
   - ดำเนินการทุก Role อัตโนมัติ แบ่งเป็น 4 Phase
   - หยุดที่ Checkpoint ทุก Phase ให้ผู้ใช้ review + approve

**Workflow:**
```
กรอก requirement_template.md
        ↓
AI ตรวจสอบ → ข้อมูลครบ? → ถ้าไม่ครบ → ถามเพิ่ม
        ↓
Phase 1: Requirements → Architecture → UX/UI → Sprint Planning
        ↓ ⏸️ Checkpoint 1 (review & approve + review Sprint Plan)
Phase 2: พัฒนาแบบ Sprint-based (ทำทีละ Sprint)
        ├─ Sprint N: Development → Code Review → Security
        ↓ ⏸️ Sprint Review (review ผลงานแต่ละ Sprint)
        └─ วนจนครบทุก Sprint
        ↓ ⏸️ Checkpoint 2 (review ภาพรวมทั้งหมด)
Phase 3: QA Testing → DevOps → Documentation
        ↓ ⏸️ Checkpoint 3 (review & approve)
Phase 4: Project Summary → ส่งมอบทั้งหมด (พร้อมสรุปรายSprint)
```

**Sprint-based Development:**
- Phase 1 จะแบ่งงานเป็น Sprint (2 สัปดาห์/Sprint)
- Sprint 1 เน้น Quick Wins — ฟีเจอร์หลักที่เห็นผลเร็ว
- แต่ละ Sprint มี Sprint Review ให้ตรวจสอบก่อนไป Sprint ถัดไป
- ช่วยจัดการ Context Window ได้ดี เพราะแบ่งงานเป็นส่วนย่อย

**อ้างอิง**: `.ai-prompts/auto-pipeline-prompt.md`

---

### Mode 2: Manual (เลือกทำทีละ Role)

เหมาะสำหรับงานเฉพาะด้าน หรือต้องการควบคุมทุกขั้นตอน

**ขั้นตอน:**

1. Fill in the Project Information above
2. Copy the relevant prompt from `.ai-prompts/` for the role you need
3. Replace `[placeholders]` with your project specifics
4. Use the deliverable templates in `templates/` to structure outputs
5. Follow the workflow order defined below

---

## Workflow Order

```
Requirement Analyst → System Architect → UX/UI Designer → Developer
                           ↓                                  ↓
                    Security Engineer              Code Reviewer
                           ↓                           ↓
                       QA/Tester ← ─────────── Security Scan
                           ↓
                    DevOps Engineer → Production
                           ↓
                    Technical Writer (continuous)
                    Product Owner (orchestrates all)
```

## Role Prompts Directory

| # | Role | Prompt File | Template Dir |
|---|------|-------------|--------------|
| - | **Auto-Pipeline** | `.ai-prompts/auto-pipeline-prompt.md` | All templates |
| 1 | Requirement Analyst | `.ai-prompts/01-requirements/prompt.md` | `templates/requirements/` |
| 2 | System Architect | `.ai-prompts/02-architecture/prompt.md` | `templates/architecture/` |
| 3 | UX/UI Designer | `.ai-prompts/03-ux-ui/prompt.md` | `templates/ux-ui/` |
| 4 | Software Developer | `.ai-prompts/04-development/prompt.md` | `templates/development/` |
| 5 | Code Reviewer | `.ai-prompts/05-code-review/prompt.md` | `templates/code-review/` |
| 6 | Security Engineer | `.ai-prompts/06-security/prompt.md` | `templates/security/` |
| 7 | QA/Tester | `.ai-prompts/07-qa-testing/prompt.md` | `templates/qa-testing/` |
| 8 | DevOps/CICD Engineer | `.ai-prompts/08-devops/prompt.md` | `templates/devops/` |
| 9 | Technical Writer | `.ai-prompts/09-documentation/prompt.md` | `templates/documentation/` |
| 10 | Product Owner/PM | `.ai-prompts/10-project-management/prompt.md` | `templates/project-management/` |

## Input Files

| File | Purpose |
|------|---------|
| `requirement_template.md` | แบบฟอร์มให้ผู้ใช้กรอกข้อมูลโครงการ (ใช้กับ Auto-Pipeline) |

## Progress Tracking

ในโหมด Auto-Pipeline ไฟล์ `templates/project-management/progress-dashboard.md` จะถูกสร้างและอัปเดตอัตโนมัติตลอดกระบวนการ เป็น **Single Source of Truth** ให้ทุก Role เห็นความคืบหน้าเดียวกัน

| อัปเดตเมื่อ | สิ่งที่อัปเดต |
|------------|-------------|
| Role เสร็จงาน | Role Completion table + Activity Log + Deliverables Registry |
| Sprint เสร็จ | Sprint Progress table + Overall % |
| Checkpoint ผ่าน | Phase Progress table |
| ตัดสินใจสำคัญ | Key Decisions log |
| พบปัญหา | Issues & Blockers log |
| Pipeline เสร็จ | Definition of Done checklist + Progress = 100% |

> ในโหมด Manual ให้อัปเดต progress-dashboard.md เองหลังจาก Role เสร็จงาน

---

## Definition of Done

Every feature/sprint must satisfy ALL of the following before release:

- [ ] Requirements approved by Stakeholder
- [ ] Design Review passed
- [ ] Code passed Code Review and Security Scan
- [ ] Unit Test Coverage >= 80%
- [ ] QA Testing passed all critical test cases
- [ ] Security Assessment: no Critical/High vulnerabilities
- [ ] Documentation complete
- [ ] Deployed to Production successfully
- [ ] Monitoring & Alerting operational

## Coding Standards

- Follow Clean Code Principles: SOLID, DRY, KISS
- Git branching: Git Flow or Trunk-based (define per project)
- Commit messages: Conventional Commits format
- PR process: All changes require review before merge
- Test coverage minimum: 80%

## Tech Stack Convention

Define your tech stack in `templates/architecture/tech-stack.md` after the Architecture phase.
All team members must reference this document for consistency.
