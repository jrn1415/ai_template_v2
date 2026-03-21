# คำแนะนำการปรับปรุง AI Template v2
**วันที่วิเคราะห์:** 2026-02-26
**อัปเดตล่าสุด:** 2026-03-21
**วิเคราะห์โดย:** AI Development SDLC Expert (Claude Sonnet 4.6)

---

## สถานะการปรับปรุง (Progress Tracker)

| # | ด้าน | สถานะ | วันที่เสร็จ |
|---|------|--------|------------|
| 1 | Prompt Engineering Quality | ✅ **เสร็จแล้ว** | 2026-02-27 |
| 2 | Context Window & Memory Management | ✅ **เสร็จแล้ว** | 2026-03-21 |
| 3 | AI Model Selection Guide | ✅ **เสร็จแล้ว** | 2026-03-21 |
| 4 | Output Validation & Quality Gates | ✅ **รวมอยู่ใน ด้านที่ 1** | 2026-02-27 |
| 5 | Real-World Integration Gap | ✅ **เสร็จแล้ว** | 2026-03-21 |
| 6 | Iteration & Rejection Handling | ✅ **เสร็จแล้ว** | 2026-03-21 |
| 7 | Example Output & Reference Documents | ✅ **เสร็จแล้ว** | 2026-03-21 |
| + | **Company Standards (bonus)** | ✅ **เสร็จแล้ว** | 2026-02-27 |
| ++ | **Pragmatic TDD (bonus)** | ✅ **เสร็จแล้ว** | 2026-02-27 |
| +++ | **Requirement Template Enhancement (bonus)** | ✅ **เสร็จแล้ว** | 2026-02-27 |
| ++++ | **R6 Architecture Review Gate (bonus)** | ✅ **เสร็จแล้ว** | 2026-02-27 |
| +++++ | **Agent Execution Protocol — R4 & R7 (bonus)** | ✅ **เสร็จแล้ว** | 2026-02-27 |
| ++++++ | **Thai Comments Rule — R4 (bonus)** | ✅ **เสร็จแล้ว** | 2026-02-27 |
| +++++++ | **Presentation Files v1-v4 (bonus)** | ✅ **เสร็จแล้ว** | 2026-02-27 |
| ++++++++ | **Audit Fix Round 1 — Consistency + Quality + Cleanup** | ✅ **เสร็จแล้ว** | 2026-03-21 |
| +++++++++ | **Audit Fix Round 2 — Context Mgmt + Rejection + Tool Integration + Model Guide + Examples** | ✅ **เสร็จแล้ว** | 2026-03-21 |

---

## สรุป Repository

Repository นี้คือ **AI-Integrated SDLC Template** — ระบบจำลองทีมพัฒนาซอฟต์แวร์ครบ 10 Role โดยใช้ AI เป็นตัวขับเคลื่อน รองรับทั้งโหมด Auto-Pipeline และ Manual พร้อม Template ครบ 50+ ไฟล์ รองรับ 2 ภาษา (ไทย/อังกฤษ)

**จุดแข็งที่มีอยู่แล้ว:**
- ครอบคลุม SDLC ครบทุก Phase
- มี Template พร้อมใช้ 50+ ไฟล์
- รองรับ 2 Mode (Auto-Pipeline / Manual)
- มี Progress Dashboard เป็น Single Source of Truth
- รองรับ 2 ภาษา (ไทย / อังกฤษ)

---

## 7 ด้านที่ควรปรับปรุง

### ด้านที่ 1 — Prompt Engineering Quality ✅ เสร็จแล้ว

**ปัญหาที่พบ:**
- Prompt ในแต่ละ Role ขาด chain-of-thought structure
- ไม่มี few-shot examples แสดงตัวอย่าง output ที่ดี
- ไม่มี output format enforcement ทำให้ AI ตอบ inconsistent

**สิ่งที่ทำไปแล้ว (2026-02-27):**

#### Phase A — Full Rewrite (11 ไฟล์)
Rewrite prompt ทุกไฟล์ใหม่ทั้งหมด เพิ่มโครงสร้างมาตรฐาน 7 Sections:

| Section | เนื้อหา |
|---------|---------|
| Section 1 | Role Identity & Expertise — ประกาศ persona + mindset |
| Section 2 | Auto Context Injection — สั่ง AI อ่านไฟล์จาก Role ก่อนหน้าอัตโนมัติ |
| Section 3 | Thinking Protocol (Chain-of-Thought) — 5-8 ขั้นตอน reasoning ก่อน output |
| Section 4 | Core Instructions — เนื้อหาหลักที่ปรับปรุงจากของเดิม |
| Section 5 | Few-Shot Example (TechShop E-commerce) — ตัวอย่าง output ที่ดีทุก Role |
| Section 6 | Output Format Schema — บังคับโครงสร้าง output ด้วย [REQUIRED] tags |
| Section 7 | Self-Validation & Handoff Digest — AI ตรวจงานตัวเองก่อน handoff |

**ไฟล์ที่ Rewrite ครบ:**
- `.ai-prompts/01-requirements/prompt.md`
- `.ai-prompts/02-architecture/prompt.md`
- `.ai-prompts/03-ux-ui/prompt.md`
- `.ai-prompts/04-development/prompt.md`
- `.ai-prompts/05-code-review/prompt.md`
- `.ai-prompts/06-security/prompt.md`
- `.ai-prompts/07-qa-testing/prompt.md`
- `.ai-prompts/08-devops/prompt.md`
- `.ai-prompts/09-documentation/prompt.md`
- `.ai-prompts/10-project-management/prompt.md`
- `.ai-prompts/auto-pipeline-prompt.md`

**Reference Project:** TechShop E-commerce (IT/Electronics ขาย + Stripe + PromptPay) ใช้เป็น few-shot example เดียวกันทุก Role เพื่อความ consistent

#### Phase B — Quality Audit & Fine-tuning (10 issues)
หลัง rewrite เสร็จ รัน audit พบ 10 ประเด็นและแก้ทั้งหมด:

**Critical (C)**
| ID | ปัญหา | การแก้ | ไฟล์ |
|----|-------|--------|------|
| C1 | "แก้ไขโค้ดอัตโนมัติ" เป็น promise ที่ไม่จริง | เปลี่ยนเป็น "ระบุปัญหา เสนอ code snippet และ flag ที่ต้อง human judgment" | auto-pipeline |
| C2 | Handoff Digest format ไม่ consistent ทั้ง 9 Role | Standardize: `→`, เพิ่ม Status/Critical Items/Key Deliverables ✅ | Role 1-9 ทุกไฟล์ |
| C3 | Section naming ใน auto-pipeline ไม่ match กับ Role prompts | เพิ่ม "SECTION 1-5:" prefix ให้ตรงกับ individual roles | auto-pipeline |

**High (H)**
| ID | ปัญหา | การแก้ | ไฟล์ |
|----|-------|--------|------|
| H1 | Risk scoring สับสน: Role1 ใช้ 1-25, Role6 ใช้ CVSS 0-10 | เพิ่ม Note อธิบายว่าทั้งสองระบบต่างกันและเหมาะกับบริบทของตัวเอง | 01-requirements, 06-security |
| H2 | Role 4 ไม่มีตัวอย่าง DB migration จริงๆ | เพิ่ม SQL migration ตัวอย่างครบ (cart tables + best practices) | 04-development |
| H3 | auto-pipeline ไม่มี sprint time-boxing rules | เพิ่ม 5 ข้อ: sprint สิ้นสุดตามกำหนด, carry over rules, carry>30% ให้แจ้ง | auto-pipeline |
| H4 | Role 6 Security ไม่มีแนะนำว่าอ่านโค้ดไฟล์ไหนก่อน | เพิ่ม File Prioritization Guide: P1 (auth/payment/input) → P2 (user/admin/DB) → P3 | 06-security |

**Medium (M)**
| ID | ปัญหา | การแก้ | ไฟล์ |
|----|-------|--------|------|
| M1 | Role 4 มีประสบการณ์ "8 ปี" ต่างจาก Role อื่นที่ใช้ 10+ ปี | เปลี่ยนเป็น "10+ ปี" | 04-development |
| M2 | bcrypt cost 12 ไม่มีอธิบายว่าทำไม | เพิ่ม "cost 12 ≈ 250ms/hash ป้องกัน brute force — OWASP recommendation" | 04-development, 06-security |
| M3 | ไม่มี guidance ถ้า API spec เปลี่ยนกลาง Sprint | เพิ่ม API Versioning Policy: ADR required, breaking change → v2, notify team | 04-development |

**ไฟล์ที่ต้องแก้:** `.ai-prompts/*/prompt.md` ทุกไฟล์
**ความยาก:** ปานกลาง | **ผลกระทบ:** สูงมาก

---

### ด้านที่ 2 — Context Window & Memory Management

**ปัญหาที่พบ:**
- Auto-Pipeline ไม่มี strategy รับมือ context overflow เมื่อโปรเจกต์ใหญ่
- ไม่มี state persistence ข้ามเซสชัน AI
- ไม่มีการ summarize/compress ข้อมูลจาก Role ก่อนหน้าก่อนส่งต่อ

**แนวทางปรับปรุง:**
- เพิ่ม **Context Summary Protocol** — สรุปสิ่งสำคัญก่อน handoff ทุกครั้ง
- เพิ่ม **Handoff Digest Template** — เอกสารสรุปสั้นๆ ระหว่าง Role
- เพิ่ม **Session Resume Guide** — วิธีเริ่มต่อเมื่อ context หาย

**ไฟล์ที่ต้องสร้างเพิ่ม:**
- `docs/context-management.md`
- `templates/handoff-digest.md`

**ความยาก:** สูง | **ผลกระทบ:** สูงมาก

---

### ด้านที่ 3 — AI Model Selection Guide

**ปัญหาที่พบ:**
- ไม่มีคำแนะนำว่าควรใช้ AI Model ไหนกับ Role ไหน
- ผู้ใช้อาจเสียค่าใช้จ่ายเกินจำเป็น หรือได้ผลลัพธ์ไม่ดีพอ

> **บริษัทนี้ใช้ Gemini Enterprise** — แนะนำ Model จาก Google Gemini family เป็นหลัก

**ตัวอย่างการจับคู่ที่เหมาะสม (Gemini Enterprise):**

| Role | งาน | Model แนะนำ | เหตุผล |
|------|-----|-------------|--------|
| 1 - Requirements | วิเคราะห์ความต้องการ | Gemini [latest Pro model] | Deep reasoning + analysis ครบ |
| 2 - Architecture | ออกแบบระบบ | Gemini [latest Pro model] | Reasoning ลึก + context window ใหญ่ |
| 3 - UX/UI | สร้าง wireframe | Gemini [latest Pro model] | Multimodal (อ่านรูปได้) + creative |
| 4 - Developer | เขียนโค้ด | Gemini [latest Pro model] | Code generation ยอดเยี่ยม + long context |
| 5 - Code Review | ตรวจโค้ด | Gemini [latest Pro model] | Analysis ลึก + เข้าใจ context โค้ดทั้งหมด |
| 6 - Security | OWASP/STRIDE | Gemini [latest Pro model] | Reasoning ลึก + อ่าน codebase ยาว |
| 7 - QA | รัน test + เขียน test cases | Gemini [latest Pro model] | Agent execution + วิเคราะห์ผล test |
| 8 - DevOps | สร้าง CI/CD config | Gemini [latest Pro model] | Config generation + infra knowledge |
| 9 - Tech Writer | เขียนเอกสาร | Gemini [latest Pro model] | Structured writing + synthesis จากทุก Role |
| 10 - PM | สรุปโปรเจกต์ | Gemini [latest Pro model] | Synthesis + dashboard update ครบ |

**Gemini Model Reference (2026):**

| Model | จุดเด่น | เหมาะกับ |
|-------|---------|---------|
| **Gemini [latest Pro model]** | Reasoning สูงสุด, context window ขนาดใหญ่, multimodal | ทุก Role — model หลักของบริษัท |

**แนวทางปรับปรุง:**
- สร้าง `docs/model-selection-guide.md` พร้อม cost/quality tradeoff matrix สำหรับ Gemini Enterprise
- เพิ่ม note ใน prompt แต่ละ Role ระบุ recommended model

**ความยาก:** ต่ำ | **ผลกระทบ:** ปานกลาง

---

### ด้านที่ 4 — Output Validation & Quality Gates

**ปัญหาที่พบ:**
- ไม่มีกลไกตรวจสอบว่า output ของ AI ครบและถูกต้องตาม template
- Checkpoint ปัจจุบันพึ่ง human judgment ล้วนๆ โดยไม่มีเกณฑ์ชัดเจน
- AI อาจส่งงานไม่ครบแต่ดูเหมือนครบ

**แนวทางปรับปรุง:**
- เพิ่ม **Automated Validation Checklist Prompt** — ให้ AI ตรวจงานตัวเองก่อน handoff
- เพิ่ม **AI Self-Review Step** ใน auto-pipeline-prompt.md
- กำหนด minimum quality threshold ต่อ Role ให้ชัดเจน

**ตัวอย่าง Self-Review Prompt:**
```
ก่อน handoff ให้ Role ถัดไป ให้ตรวจสอบ:
[ ] Output ครบทุก section ตาม template ไหม?
[ ] ไม่มี [PLACEHOLDER] หลงเหลือไหม?
[ ] ข้อมูลสอดคล้องกับ input จาก Role ก่อนหน้าไหม?
[ ] Deliverables list ครบไหม?
```

**ไฟล์ที่ต้องแก้:** `.ai-prompts/auto-pipeline-prompt.md`
**ความยาก:** ปานกลาง | **ผลกระทบ:** สูง

---

### ด้านที่ 5 — Real-World Integration Gap 🔄 บางส่วนแล้ว

**ปัญหาที่พบ:**
- Template ออกแบบมาสำหรับ "document-first" แต่ไม่มี bridge ไปสู่การใช้งานจริง
- ไม่มี guide สำหรับการ integrate กับ tools จริง เช่น GitHub, Jira, Figma, Cursor IDE
- Role 4 (Developer) บอกให้ "เขียนโค้ด" แต่ไม่ได้บอกว่าจะจัดการ file structure อย่างไร

**สิ่งที่ทำไปแล้ว (2026-02-27) — Agent Execution Protocol:**
- เพิ่ม `⚡ Agent Execution Mode` ใน R4 (Developer) และ R7 (QA)
- R4 ตอนนี้รันคำสั่ง build/test จริงผ่าน shell (`dotnet build`, `dotnet test`, `npm run build` ฯลฯ) และรายงาน terminal output จริง
- R7 ตอนนี้เริ่ม app จริง (health check loop), รัน E2E tests (Playwright/Cypress), API tests (Newman), Performance tests (k6), Security scans (OWASP ZAP) และรายงาน actual results
- รองรับ Agent frameworks หลายตัว: Claude Code, Cursor, Devin, OpenHands, Windsurf (ไม่ lock-in กับ Claude Code เท่านั้น)
- ดู [Section ด้านที่ +++++ (Agent Execution Protocol)](#ด้านที่------agent-execution-protocol--r4--r7-bonus) ด้านล่าง

**ยังต้องทำ (Remaining):**
- **Tool Integration Guide** สำหรับ tools ภายนอก:
  - GitHub: template สำหรับ Issues, PR, Actions
  - Jira/Linear: วิธี export Sprint Plan ไปสร้าง tickets
  - Figma: วิธีใช้ wireframe output จาก Role 3
- ไฟล์ที่ยังต้องสร้าง:
  - `docs/tool-integration-guide.md`

**ความยาก:** สูง | **ผลกระทบ:** สูง | **สถานะ:** 🔄 50% เสร็จ

---

### ด้านที่ 6 — Iteration & Rejection Handling

**ปัญหาที่พบ:**
- ไม่มี process ชัดเจนสำหรับกรณีที่ผู้ใช้ reject งานที่ Checkpoint
- ไม่รู้ว่าต้องเริ่ม Role ใหม่ทั้งหมด หรือแก้เฉพาะจุด
- ไม่มี partial retry protocol

**แนวทางปรับปรุง:**
- เพิ่ม **Rejection Handling Flow** — decision tree เมื่องานถูก reject:
  ```
  Reject at Checkpoint
      ├─ Major issues (>50% เปลี่ยน) → redo ทั้ง Role
      ├─ Minor issues (<50% เปลี่ยน) → partial revision
      └─ Specific section → targeted fix prompt
  ```
- เพิ่ม **Revision Request Template** — format ที่ชัดเจนสำหรับบอก AI ว่าต้องแก้อะไร

**ไฟล์ที่ต้องแก้:** `.ai-prompts/auto-pipeline-prompt.md`
**ไฟล์ที่ต้องสร้างเพิ่ม:** `docs/rejection-handling.md`
**ความยาก:** ต่ำ | **ผลกระทบ:** ปานกลาง

---

### ด้านที่ 7 — Example Output & Reference Documents

**ปัญหาที่พบ:**
- Template ทุกตัวเป็น blank placeholder ไม่มี sample output จริงเลย
- ผู้ใช้ใหม่ไม่รู้ว่าผลลัพธ์ที่ดีควรเป็นอย่างไร
- ไม่มี reference project สำหรับ benchmark quality

**แนวทางปรับปรุง:**
- สร้าง `examples/` directory พร้อม sample project แบบ end-to-end
- ตัวอย่างโปรเจกต์ที่เหมาะ: **Todo App with Auth** (เรียบง่าย แต่ครอบคลุมทุก Role)
- แต่ละ Role ควรมี 1 completed example output เป็น reference

**โครงสร้างที่แนะนำ:**
```
examples/
└── todo-app-sample/
    ├── 01-requirements/       # ตัวอย่าง output Role 1
    ├── 02-architecture/       # ตัวอย่าง output Role 2
    ├── 03-ux-ui/              # ตัวอย่าง output Role 3
    ├── 04-development/        # ตัวอย่าง output Role 4
    ├── 05-code-review/        # ตัวอย่าง output Role 5
    ├── 06-security/           # ตัวอย่าง output Role 6
    ├── 07-qa-testing/         # ตัวอย่าง output Role 7
    ├── 08-devops/             # ตัวอย่าง output Role 8
    ├── 09-documentation/      # ตัวอย่าง output Role 9
    └── 10-project-management/ # ตัวอย่าง output Role 10
```

**ความยาก:** ปานกลาง | **ผลกระทบ:** สูง

---

---

### ด้านที่ + — Company Standards (Bonus) ✅ เสร็จแล้ว

> งานนี้ไม่ได้อยู่ใน 7 ด้านเดิม แต่ทำเพิ่มตามคำขอของผู้ใช้

**ปัญหาที่พบ:**
- Template ไม่มี baseline standards ของบริษัท ทุก project ต้องกำหนด coding rules เองใหม่ทุกครั้ง
- ไม่มีรายการ approved tech stack — AI อาจเลือก technology ที่บริษัทไม่มี expertise
- Role 4 (Developer) และ Role 5 (Code Review) ไม่รู้ว่าต้อง follow convention อะไร

**สิ่งที่ทำไปแล้ว (2026-02-27):**

#### Phase A — สร้าง `standards/` Folder

**ไฟล์ที่สร้างใหม่:**

| ไฟล์ | เนื้อหา |
|------|--------|
| `standards/coding-standards.md` | Naming conventions (C#/JS/Python), Git & Commit format, Testing standards, Security baseline (OWASP), Language-specific rules (C#/.NET 10, TypeScript, Python, Go), Code Review checklist |
| `standards/tech-stack-catalog.md` | Approved/Conditional/Not Approved tech stack ทุก layer: Frontend, Backend, DB, DevOps, Auth, Messaging, Monitoring, AI/LLM, Default Stack recommendation |

#### Phase B — ปรับให้ reflect .NET 10 เป็น Primary Backend

หลังจากผู้ใช้ระบุว่าบริษัทใช้ **.NET 10 (LTS)** เป็น backend หลัก ปรับ 2 ไฟล์:

**`standards/tech-stack-catalog.md`:**
| Section | การเปลี่ยนแปลง |
|---------|--------------|
| Backend Framework | ASP.NET Core 10 (Minimal API + MVC) → ✅ Approved Default / Node.js, Python → ⚠️ Conditional |
| API Design | เพิ่ม `System.Text.Json` (default), Hot Chocolate สำหรับ GraphQL |
| ORM | เพิ่ม **EF Core 10** + **Dapper** เป็น ✅ Approved พร้อม guideline เลือกใช้ |
| IaC | เพิ่ม **Bicep** สำหรับ Azure deployment |
| Auth | เพิ่ม **ASP.NET Core Identity** + **JWT Bearer (.NET)** + Duende IdentityServer |
| Messaging | เพิ่ม **MassTransit + RabbitMQ** + **Hangfire** เป็น ✅ Approved Default (.NET) |
| Default Stack | ปรับเป็น .NET 10 เป็น backend หลัก |

**`standards/coding-standards.md`:**
| Section | การเปลี่ยนแปลง |
|---------|--------------|
| Naming table | เพิ่มคอลัมน์ภาษา — C# ใช้ PascalCase สำหรับ methods, `_camelCase` สำหรับ private fields |
| Section 5 | เพิ่ม **C# / .NET 10 block** เป็น primary: Nullable, records, async/await patterns, DI, project structure (Clean Architecture), testing packages (xUnit + FluentAssertions + NSubstitute + Testcontainers + Bogus), linting (dotnet format + Roslyn + SonarAnalyzer) |
| Test Naming | เพิ่มรูปแบบ xUnit: `MethodName_Scenario_ExpectedResult` |
| Security | เพิ่ม `dotnet list package --vulnerable` ใน dependency scan |

#### Phase C — Wire standards/ เข้า Prompts และ CLAUDE.md

| ไฟล์ | สิ่งที่เพิ่ม |
|------|------------|
| `.ai-prompts/02-architecture/prompt.md` | Section 2: `READ: standards/tech-stack-catalog.md` + คำอธิบาย Conditional → ADR |
| `.ai-prompts/04-development/prompt.md` | Section 2: `READ: standards/coding-standards.md` + override policy |
| `.ai-prompts/05-code-review/prompt.md` | Section 2: `READ: standards/coding-standards.md` + pointer ไป sections ที่ relevant |
| `CLAUDE.md` | แทนที่ section "Coding Standards" เดิมด้วย Company Standards table + override policy |

---

---

### ด้านที่ ++ — Pragmatic TDD (Bonus) ✅ เสร็จแล้ว

> งานนี้ทำต่อเนื่องจาก Company Standards โดยผู้ใช้ต้องการเปลี่ยน testing approach เป็น TDD

**ปัญหาที่พบ:**
- `coding-standards.md` พูดถึง TDD แบบ "soft" — ใช้คำว่า "เมื่อทำได้" ซึ่งทำให้ไม่มีการบังคับใช้จริง
- Role 4 Thinking Protocol เขียน test หลัง implement (test-after โดยธรรมชาติ)
- ไม่มี guidance ว่า layer ไหนต้อง TDD, layer ไหน test-after ได้
- เมื่อใช้ AI ช่วยเขียน code — AI มักเขียน test และ implementation พร้อมกัน (TDD ปลอม)

**สิ่งที่ทำไปแล้ว (2026-02-27):**

#### ไฟล์ที่เปลี่ยน: 3 ไฟล์

**`standards/coding-standards.md` — Section 3 (rewrite ทั้งหมด)**
| สิ่งที่เพิ่ม | รายละเอียด |
|------------|-----------|
| Red→Green→Refactor cycle | อธิบาย 3 ขั้นตอนพร้อม 🔴🟢🔵 visual indicator |
| AI-specific warning | บังคับแยก 2 prompt: prompt แรก = test only, prompt สอง = implementation |
| Pragmatic TDD layer table | Service/Repository = ✅ บังคับ TDD / Controller/UI = ⚠️ test-after / Config/Migration = ❌ ไม่ต้อง |
| Test Naming + TDD markers | เพิ่ม comment 🔴🟢🔵 ใน code example ให้เห็น workflow ชัด |

**`.ai-prompts/04-development/prompt.md` — 3 จุด**
| จุดที่เปลี่ยน | รายละเอียด |
|-------------|-----------|
| Section 1 (Role Identity) | เปลี่ยน "เขียน test ก่อนเมื่อทำได้" → "บังคับ Red→Green→Refactor ใน Service/Domain layer" |
| Section 3 (Thinking Protocol) | แยก Step 5 🔴 (Write Failing Tests) ออกก่อน Step 6 🟢 (Implement) และ Step 7 🔵 (Refactor) — เพิ่มเป็น 8 steps |
| Section 4.3 (Testing Standards) | rewrite ใหม่ทั้งหมด — TDD workflow loop, layer-by-layer guide, AI Warning (2-prompt rule) |

**`.ai-prompts/auto-pipeline-prompt.md` — Role 4 Chain-of-Thought**
| สิ่งที่เปลี่ยน | รายละเอียด |
|--------------|-----------|
| Chain-of-Thought | ปรับจาก 7 → 8 steps พร้อม 🔴🟢🔵 labels ชัดเจน |
| AI TDD Rule | เพิ่ม note ใต้ chain-of-thought: "แยก Step 4 และ 5 เป็น 2 รอบแยกกัน" |
| Self-Validation checklist | เพิ่มข้อ: "Tests เขียนก่อน implementation สำหรับ Service/Repository layer" + "ทุก test ผ่าน (ไม่มี skip หรือ commented-out)" |

---

### ด้านที่ +++ — Requirement Template Enhancement (Bonus) ✅ เสร็จแล้ว

> เพิ่มตามการวิเคราะห์ว่า `requirement_template.md` ขาด input สำคัญที่ auto-pipeline ต้องการ

**ปัญหาที่พบ:**
- ไม่มีเกณฑ์วัดความสำเร็จ (KPIs) — Role 1 เขียน Business Objectives ได้ไม่ครบ
- ไม่มี Sprint/Timeline Expectation — auto-pipeline แบ่ง Sprint ได้ไม่แม่น
- ไม่รู้ทักษะทีม — Architect เลือก tech stack โดยไม่รู้ expertise ทีม
- Section 4 (Tech Stack) ไม่ link ไป `standards/tech-stack-catalog.md`
- ไม่มี section สำหรับ Notification & Reporting ซึ่งพบบ่อยในโปรเจกต์จริง

**สิ่งที่ทำไปแล้ว (2026-02-27):**

| จุดที่เพิ่ม | รายละเอียด | Section |
|-----------|-----------|---------|
| **KPIs row** | เพิ่ม "เกณฑ์วัดความสำเร็จ (KPIs)" เป็น required field (*) | Section 1 |
| **Tech Stack note** | เพิ่ม note ชี้ไป `standards/tech-stack-catalog.md` พร้อม ADR policy | Section 4 |
| **Team Background** | เพิ่ม row "ทักษะ/Tech ที่ทีมถนัด" | Section 8 |
| **Sprint Expectation** | เพิ่ม row "จำนวน Sprint ที่ต้องการ" และ "MVP ต้องพร้อมเมื่อ" | Section 8 |
| **Notification & Reporting** | เพิ่ม subsection: Notification channels table + Dashboard/Reports table | Section 9 |
| **Checklist** | อัปเดต checklist สะท้อน required fields ใหม่ (KPIs, Sprint, Team skill) | Checklist |

---

---

### ด้านที่ ++++ — R6 Architecture Review Gate (Bonus) ✅ เสร็จแล้ว

> เพิ่ม Security Review Gate ระหว่าง R2 (Architect) และ R3 (UX/UI) + R4 (Developer)

**ปัญหาที่พบ:**
- Workflow เดิม: R2 → R3/R4 โดยตรง — ไม่มี Security review architecture ก่อนออกแบบ UI หรือเขียนโค้ด
- ถ้าพบ Security issue ในช่วงท้าย (R6 Phase 2) จะต้องแก้ architecture ซึ่งแพงมาก
- R6 (Security Engineer) เดิมมีแค่ Phase 2 (Code Scan) ไม่มี Phase 1 (Architecture Review)

**สิ่งที่ทำไปแล้ว (2026-02-27):**

| ไฟล์ | สิ่งที่เพิ่ม |
|------|------------|
| `.ai-prompts/02-architecture/prompt.md` | Section 7 Handoff เปลี่ยนจาก "→ R3/R4" เป็น "→ R6 (Architecture Review)" + Security Focus Areas checklist |
| `.ai-prompts/06-security/prompt.md` | เพิ่ม Mode Detection (Phase 1 vs Phase 2), Phase 1 Context Injection, Phase 1 Thinking Protocol (7 steps), Phase 1 Output Schema, Phase 1 Handoff Digest (APPROVED→R3+R4 / ISSUES→R2) |
| `.ai-prompts/auto-pipeline-prompt.md` | Insert `Role 6 (Phase 1): Security Engineer — Architecture Review` ระหว่าง Role 2 และ Role 3 พร้อม Gate Logic |

**ผล:** Gate ใหม่ R2→R6(Phase1)→[R3+R4] ทำให้ Security ถูก review ตั้งแต่ Architecture stage — ลดต้นทุนแก้ไขในระยะหลัง

---

### ด้านที่ +++++ — Agent Execution Protocol — R4 & R7 (Bonus) ✅ เสร็จแล้ว

> เปลี่ยน R4 (Developer) และ R7 (QA) จาก document-generation เป็น actual command execution

**ปัญหาที่พบ:**
- R4 เดิม: AI "เขียนโค้ด" แต่ไม่รัน build/test จริง — ไม่รู้ว่าโค้ดที่เขียนผ่านหรือไม่
- R7 เดิม: AI "เขียน test cases" แต่ไม่รัน test จริง — ไม่รู้ผลลัพธ์จริง
- AI agents ปัจจุบัน (Claude Code, Cursor, Devin ฯลฯ) มีความสามารถ shell execution — แต่ไม่ได้ระบุในระบบ

**สิ่งที่ทำไปแล้ว (2026-02-27):**

**R4 (Developer) — `.ai-prompts/04-development/prompt.md`:**
| สิ่งที่เพิ่ม | รายละเอียด |
|------------|-----------|
| `⚡ Agent Execution Mode` declaration | Section 1 ระบุชัดว่าต้องรันจริง |
| `⚡ RUN:` markers ใน Steps 5-7 | TDD loop พร้อม shell commands จริง |
| Section 4.6 Agent Execution Protocol | Tech Stack Detection table (*.csproj=.NET / package.json=Node / ฯลฯ), TDD Execution Loop (`RUN→FAIL → RUN→GREEN → RUN build+test+coverage`), Error Recovery Protocol |
| Actual Output Format | Self-Validation + Handoff ต้องมี terminal output จริง (exit code, coverage %) |

**R7 (QA) — `.ai-prompts/07-qa-testing/prompt.md`:**
| สิ่งที่เพิ่ม | รายละเอียด |
|------------|-----------|
| `⚡ Agent Execution Mode` declaration | Section 1 ระบุชัดว่าต้องรันจริง |
| App Startup Protocol | Health check loop ก่อนรัน test: `curl /health` ทุก 5 วินาที max 60s |
| Test Tool Commands table | Playwright/Cypress (E2E), Newman (API), k6/Artillery (Performance), OWASP ZAP (Security) |
| Actual Results Format | Output schema ต้องมี actual terminal output + pass/fail/skip counts |
| Error Recovery Protocol | ถ้า test fail → screenshot/log → สร้าง bug report → อย่าหยุด |

**Framework-agnostic design:** ใช้ได้กับ Claude Code, Cursor, Devin, OpenHands, Windsurf — ไม่ lock-in

---

### ด้านที่ ++++++ — Thai Comments Rule — R4 (Bonus) ✅ เสร็จแล้ว

> เพิ่ม coding convention: comment ภาษาไทยใน source code

**ปัญหาที่พบ:**
- R4 prompt ไม่มี rule เกี่ยวกับภาษาของ comment — AI อาจ comment เป็นภาษาอังกฤษหรือไม่ comment เลย
- ทีมไทยอ่าน comment ภาษาไทยได้เข้าใจเร็วกว่า โดยเฉพาะในส่วน business logic

**สิ่งที่ทำไปแล้ว (2026-02-27):**

ใน `.ai-prompts/04-development/prompt.md` Section 4.2 เพิ่ม:

```
// Comments: เขียนภาษาไทยเสมอ — อธิบายเฉพาะ "why" ไม่ใช่ "what"
// ✅ ดี: // ตรวจสอบก่อนว่า cart ไม่ว่างเปล่า เพราะ Stripe จะ error ถ้า amount = 0
// ❌ ไม่ดี: // Check if cart is empty
```

**Rule:**
- Comment ภาษาไทยทุกครั้ง
- อธิบาย "why" (ทำไม) ไม่ใช่ "what" (ทำอะไร)
- ใช้ทั้งใน method body และ class-level summary

---

### ด้านที่ +++++++ — Presentation Files v1-v4 (Bonus) ✅ เสร็จแล้ว

> สร้าง presentation HTML สำหรับ training / demo ระบบ

**ปัญหาที่พบ:**
- ไม่มีเอกสารสำหรับ present ระบบให้ทีม/ผู้บริหารเข้าใจภาพรวม
- README อ่านยากสำหรับ non-technical audience

**สิ่งที่ทำไปแล้ว (2026-02-27):**

| ไฟล์ | เนื้อหา | สไลด์ |
|------|---------|-------|
| `present/sdlc-template-presentation_v1.html` | Version แรก — ภาพรวม SDLC template | 13 slides |
| `present/sdlc-template-presentation_v2.html` | เพิ่มรายละเอียด workflow | 13 slides |
| `present/sdlc-template-presentation_v3.html` | ปรับ visual style (cyber/neon) | 14 slides |
| `present/sdlc-template-presentation_v4.html` | เพิ่ม Slide 14: Improvement Roadmap (5 done / 5 next) | 15 slides |

**Style:** Dark bg `#0a0a0f`, neon colors, terminal-style font, interactive navigation

**Improvement Roadmap Slide (v4) แสดง:**
- สถานะ: 5 completed (✅) / 5 pending (⬜)
- LEFT column: สิ่งที่ทำเสร็จ (green cards)
- RIGHT column: สิ่งที่รอทำ เรียงตาม ⭐ priority

---

## ตารางสรุปและลำดับความสำคัญ

| # | ด้าน | ความยาก | ผลกระทบ | สถานะ | แนะนำทำก่อน |
|---|------|---------|---------|--------|------------|
| 1 | Prompt Engineering Quality | ปานกลาง | สูงมาก | ✅ เสร็จแล้ว | ~~⭐⭐⭐~~ |
| 4 | Output Validation & Quality Gates | ปานกลาง | สูง | ✅ รวมใน ด้านที่ 1 | ~~⭐⭐~~ |
| + | Company Standards (.NET 10) | ปานกลาง | สูง | ✅ เสร็จแล้ว | — |
| ++ | Pragmatic TDD | ปานกลาง | สูง | ✅ เสร็จแล้ว | — |
| +++ | Requirement Template Enhancement | ต่ำ | ปานกลาง | ✅ เสร็จแล้ว | — |
| ++++ | R6 Architecture Review Gate | ปานกลาง | สูงมาก | ✅ เสร็จแล้ว | — |
| +++++ | Agent Execution Protocol (R4+R7) | ปานกลาง | สูงมาก | ✅ เสร็จแล้ว | — |
| ++++++ | Thai Comments Rule (R4) | ต่ำ | ปานกลาง | ✅ เสร็จแล้ว | — |
| +++++++ | Presentation Files v1-v4 | ต่ำ | ปานกลาง | ✅ เสร็จแล้ว | — |
| ++++++++ | **Audit Fix Round 1** (2026-03-21) | ปานกลาง | สูง | ✅ เสร็จแล้ว | — |
| 5 | Real-World Integration Gap | สูง | สูง | 🔄 50% (Agent Exec done, Tool Integration pending) | ⭐⭐ |
| 2 | Context Window & Memory Management | สูง | สูงมาก | ⬜ ถัดไป | ⭐⭐⭐ |
| 7 | Example Output & Reference Documents | ปานกลาง | สูง | ⬜ ถัดไป | ⭐⭐ |
| 6 | Iteration & Rejection Handling | ต่ำ | ปานกลาง | ⬜ ถัดไป | ⭐⭐ |
| 3 | AI Model Selection Guide | ต่ำ | ปานกลาง | ⬜ ถัดไป | ⭐ |

**ลำดับที่แนะนำทำต่อ:**
1. **ด้านที่ 2** (Context Management) — จำเป็นมากสำหรับโปรเจกต์ขนาดกลาง-ใหญ่
2. **ด้านที่ 6** (Rejection Handling) — ทำได้เร็ว ช่วย UX จริง เมื่อผู้ใช้ reject งาน
3. **ด้านที่ 7** (Examples) — ช่วย onboarding ผู้ใช้ใหม่มาก
4. **ด้านที่ 5** (Tool Integration ส่วนที่เหลือ) — `docs/tool-integration-guide.md`
5. **ด้านที่ 3** (Model Selection Guide) — ทำได้เร็ว ลด cost ได้ทันที

---

## Audit Fix Round 1 — 2026-03-21

### Wave 1: Consistency Fixes (I-1 ถึง I-5, Q-2)

| Fix | ไฟล์ที่แก้ | รายละเอียด |
|-----|-----------|-----------|
| I-1 | `CLAUDE.md` | เพิ่ม DBA ใน Workflow Order diagram และ Role Prompts Directory table |
| I-2 | `auto-pipeline-prompt.md` | แก้ "10 บทบาท" → "11 บทบาท" (Section 1) |
| I-3 | `README.md` | แก้ "10 roles" → "11 roles" ใน Quick Start section |
| I-4 | `README-th.md` | เพิ่ม DBA ใน workflow diagram + แก้ "10 บทบาท" → "11 บทบาท" ใน file tree |
| I-5 | `auto-pipeline-prompt.md` | เพิ่ม `Overall Progress > 20%` ให้ R6 Phase 1 (ที่ขาดหายไป) |
| Q-2 | `auto-pipeline-prompt.md` + `11-dba/prompt.md` | แก้ DBA Chain-of-Thought ให้ครบ 7 steps (เพิ่ม Step 4 Normalization, แก้ "Step 10" → "Step 7") |

### Wave 2: Quality Improvements (Q-1, Q-3, Q-4, Q-5)

| Fix | ไฟล์ที่แก้ | รายละเอียด |
|-----|-----------|-----------|
| Q-1 | `.ai-prompts/11-dba/prompt.md` | Upgrade v1.0 → v2.0: เพิ่ม Few-shot example (TechShop), Handoff Digest format มาตรฐาน, DB Security section (4.5), Agent Execution awareness, Section 5 Example, Section numbering ถูกต้อง |
| Q-3 | `templates/11-dba/db-schema.md` | Rewrite template ใหม่ทั้งหมด: เพิ่ม Normalization Decisions (Section 2), DB Security Design (Section 6), Backup & Recovery Plan (Section 8), ปรับ Table Definitions ให้ละเอียด |
| Q-4 | `.ai-prompts/04-development/prompt.md` | เพิ่ม multi-language columns ใน Layer-by-Layer Testing Guide (Node.js, Python, Go) |
| Q-5 | `docs/improvement-recommendations.md` | แก้ "Gemini 3.1 Pro" → "Gemini [latest Pro model]" (model ที่ระบุไม่มีอยู่จริง) |

### Wave 3: Template Cleanup (R-1, R-2 + Merges)

| Fix | ไฟล์ที่เปลี่ยน | รายละเอียด |
|-----|--------------|-----------|
| ลบ | `templates/03-ux-ui/usability-testing.md` | ต้องการ real users — AI ทำแทนไม่ได้อย่างมีความหมาย |
| ลบ | `templates/04-development/test-conventions.md` | ซ้ำกับ `standards/coding-standards.md` Section 3 |
| ลบ | `templates/10-project-management/status-report.md` | ซ้ำกับ progress-dashboard.md |
| Merge | `templates/01-requirements/priority-matrix.md` → `requirements-document.md` Section 8 | MoSCoW อยู่ในไฟล์เดียวกัน ลดไฟล์แยก |
| Merge | `templates/05-code-review/review-checklist.md` → `review-report.md` | Checklist รวมอยู่ท้าย review report |
| อัปเดต | 6 prompt files + auto-pipeline | ลบ/อัปเดต reference ไปยังไฟล์ที่ลบ/รวมแล้ว |

**ผลรวม:** ลด 5 ไฟล์ template | แก้ 13 จุด inconsistency | upgrade DBA prompt + template ให้ match มาตรฐาน v2.0

---

*วิเคราะห์โดย Claude Sonnet 4.6 — AI Development SDLC Expert Mode*
*อัปเดตล่าสุด: 2026-03-21 — Audit Fix Round 1 (Wave 1-3)*
