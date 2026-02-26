# Templates Guide — คู่มืออธิบายไฟล์ Template ทั้งหมด

> **47 ไฟล์** ใน 10 โฟลเดอร์ · ครอบคลุมทุกขั้นตอน SDLC
> แต่ละไฟล์ออกแบบมาให้ AI หรือทีมงานกรอกเป็น deliverable จริงของโครงการ

---

## วิธีใช้คู่มือนี้

| สัญลักษณ์ | ความหมาย |
|----------|---------|
| **เขียนโดย** | Role ที่รับผิดชอบสร้างไฟล์นี้ |
| **ใช้โดย** | Role อื่นที่อ่านไฟล์นี้เป็น input |
| **สร้างเมื่อ** | Phase / ขั้นตอนที่ควรสร้างไฟล์นี้ |

---

## 01-requirements/ — วิเคราะห์ความต้องการ (4 ไฟล์)

> สร้างโดย **Role 1 — Requirement Analyst** ใน Phase 1

---

### `requirements-document.md` — เอกสารความต้องการระบบ

**ใช้ทำอะไร:**
บันทึกความต้องการทั้งหมดของระบบอย่างเป็นทางการ ทั้ง Functional Requirements (สิ่งที่ระบบต้องทำ) และ Non-Functional Requirements (เงื่อนไขด้านคุณภาพ เช่น performance, security, scalability)

**โครงสร้างหลัก:**
- Executive Summary — สรุปภาพรวม
- Business Objectives — เป้าหมายธุรกิจพร้อม Success Metric
- Functional Requirements — จัดเป็นรายโมดูล พร้อม ID และ Acceptance Criteria
- Non-Functional Requirements — Performance, Scalability, Availability, Security, Usability
- Constraints & Assumptions — ข้อจำกัดและสมมติฐาน
- Approval Table — ลายเซ็น PO, Tech Lead, Stakeholder

**ประโยชน์:**
- เป็น "สัญญา" ระหว่างทีมพัฒนาและ Stakeholder ว่าจะสร้างอะไร
- Architect และ Developer ใช้เป็น input หลักในการออกแบบระบบ
- QA ใช้ Acceptance Criteria เพื่อเขียน Test Cases
- ลดความเข้าใจผิดที่พบบ่อยที่สุดในโครงการ IT

**ใช้โดย:** Role 2 (Architect), Role 4 (Dev), Role 7 (QA)

---

### `user-story-map.md` — แผนที่ User Story

**ใช้ทำอะไร:**
จัดเรียง User Stories ในรูปแบบ 2 มิติ — แกนนอน = ลำดับการใช้งาน (User Journey), แกนตั้ง = ระดับความสำคัญ/รายละเอียด ช่วยให้เห็นภาพรวมของทุกฟีเจอร์ในคราวเดียว

**โครงสร้างหลัก:**
- Epic → Feature → User Story (ลำดับชั้น)
- Story ID, As a [user] I want [action] so that [benefit]
- Priority (Must/Should/Could/Won't) และ Story Points
- Sprint assignment

**ประโยชน์:**
- เห็น "big picture" ของระบบทั้งหมดในหน้าเดียว
- PM ใช้วางแผน Sprint — ตัดเลือกว่า Sprint ไหนทำ Story ไหน
- ทีมเห็นความเชื่อมโยงระหว่างฟีเจอร์ต่างๆ
- ง่ายต่อการสื่อสารกับ Stakeholder ที่ไม่ใช่ technical

**ใช้โดย:** Role 10 (PM), ทีมพัฒนาทั้งหมด

---

### `priority-matrix.md` — เมทริกซ์จัดลำดับความสำคัญ

**ใช้ทำอะไร:**
ประเมินและจัดลำดับฟีเจอร์ด้วยกรอบ MoSCoW (Must / Should / Could / Won't) ร่วมกับการประเมิน Impact vs Effort เพื่อตัดสินใจว่าจะทำอะไรก่อน

**โครงสร้างหลัก:**
- MoSCoW Classification Table
- Impact vs Effort Matrix (2x2)
- MVP Definition — สิ่งที่จำเป็นสำหรับ release แรก
- Feature Backlog — สิ่งที่เลื่อนออกไป

**ประโยชน์:**
- ตัดสินใจอย่างมีเหตุผล ไม่ใช่แค่ตามความชอบ
- ป้องกัน scope creep — มี record ว่า feature ไหนจงใจไม่ทำ
- PM และ Stakeholder ใช้ตัดสินใจร่วมกันได้ง่าย
- ช่วยกำหนดขอบเขต MVP ชัดเจน

**ใช้โดย:** Role 10 (PM), Stakeholder

---

### `risk-analysis.md` — วิเคราะห์ความเสี่ยง

**ใช้ทำอะไร:**
ระบุและประเมินความเสี่ยงทั้งหมดของโครงการ ทั้งด้านเทคนิค, ธุรกิจ, และทรัพยากร พร้อมแผนรับมือ (Mitigation Plan)

**โครงสร้างหลัก:**
- Risk Register Table — Risk ID, Description, Probability, Impact, Score
- Risk Matrix (Heat Map)
- Mitigation Strategy สำหรับความเสี่ยงสูง
- Risk Owner และ Review Date

**ประโยชน์:**
- ป้องกัน "surprises" ในโครงการ — รู้ล่วงหน้าว่าอะไรอาจผิดพลาด
- PM ใช้ติดตามและ escalate ความเสี่ยงที่เปลี่ยนไป
- Security Engineer ใช้เป็น input สำหรับ Threat Model
- Stakeholder เข้าใจความเสี่ยงก่อนอนุมัติโครงการ

**ใช้โดย:** Role 6 (Security), Role 10 (PM), Stakeholder

---

## 02-architecture/ — ออกแบบสถาปัตยกรรม (6 ไฟล์)

> สร้างโดย **Role 2 — System Architect** ใน Phase 1

---

### `architecture-diagram.md` — แผนผังสถาปัตยกรรมระบบ

**ใช้ทำอะไร:**
บันทึกสถาปัตยกรรมระบบทั้งหมด ตั้งแต่ระดับ High-Level (Layers, Components) ไปจนถึง Low-Level (Service interactions, Deployment topology)

**โครงสร้างหลัก:**
- System Overview — Diagram ระดับ C4 Model (Context, Container, Component)
- Technology Stack ที่เลือกใช้
- Communication patterns (REST/gRPC/Event-driven)
- Deployment Architecture (Cloud, Container, etc.)
- Scalability & Resilience patterns

**ประโยชน์:**
- Developer เข้าใจโครงสร้างระบบก่อนเขียนโค้ด
- ลดการตัดสินใจ ad-hoc ระหว่างการพัฒนา
- ใช้ onboard สมาชิกใหม่ได้เร็ว
- จุดเริ่มต้นของการ review architecture

**ใช้โดย:** Role 4 (Dev), Role 6 (Security), Role 8 (DevOps)

---

### `tech-stack.md` — รายการ Tech Stack ที่เลือกใช้

**ใช้ทำอะไร:**
บันทึกการตัดสินใจเลือก Technology สำหรับโครงการนี้โดยเฉพาะ พร้อมเหตุผลที่เลือก version ที่ใช้ และข้อตกลงของทีม

**โครงสร้างหลัก:**
- Final Tech Stack Table — Layer, Technology, Version, เหตุผล
- Project-specific overrides จาก `standards/tech-stack-catalog.md`
- ADR references สำหรับการตัดสินใจที่ต้องอธิบายเพิ่ม

**ประโยชน์:**
- ทุกคนในทีมรู้ว่าใช้ technology อะไร version อะไร
- ป้องกันการใช้ library ที่ไม่ได้รับอนุมัติ
- DevOps ใช้ตั้งค่า build pipeline และ container images
- Security Engineer ใช้ตรวจสอบ known vulnerabilities

**ใช้โดย:** Role 4 (Dev), Role 8 (DevOps), Role 6 (Security)

---

### `api-spec.md` — เอกสาร API Specification

**ใช้ทำอะไร:**
กำหนด contract ของทุก API Endpoint — method, path, request/response schema, error codes, authentication

**โครงสร้างหลัก:**
- Base URL และ Authentication method
- แต่ละ Endpoint: Method, Path, Description, Request body, Response schema, Error codes
- Pagination, Filtering, Sorting conventions
- Rate Limiting policy

**ประโยชน์:**
- Frontend และ Backend ทำงานพร้อมกันได้ (API-first development)
- QA เขียน API test cases ได้ก่อน implementation เสร็จ
- เป็นเอกสารสำหรับ third-party integrations
- ลดการ miscommunication ระหว่าง developer

**ใช้โดย:** Role 4 (Dev), Role 7 (QA), Role 9 (Tech Writer)

---

### `db-schema.md` — Database Schema

**ใช้ทำอะไร:**
กำหนดโครงสร้างฐานข้อมูลทั้งหมด — ตาราง, คอลัมน์, data types, indexes, foreign keys, constraints

**โครงสร้างหลัก:**
- Entity Relationship Diagram (ERD) แบบ text/Mermaid
- แต่ละตาราง: columns, types, constraints, indexes
- Relationships และ Cardinality
- Migration strategy

**ประโยชน์:**
- Developer เขียน migration scripts และ ORM models ได้ถูกต้อง
- ป้องกันปัญหา data integrity ตั้งแต่ออกแบบ
- DBA/DevOps ใช้ตั้งค่า database
- Security Engineer ตรวจสอบ sensitive data fields

**ใช้โดย:** Role 4 (Dev), Role 6 (Security), Role 8 (DevOps)

---

### `data-flow.md` — แผนผัง Data Flow

**ใช้ทำอะไร:**
อธิบายว่าข้อมูลไหลผ่านระบบอย่างไร ตั้งแต่ input จากผู้ใช้ → การประมวลผล → การจัดเก็บ → output เหมาะสำหรับระบบที่มีข้อมูลซับซ้อนหรือ integration หลายจุด

**โครงสร้างหลัก:**
- Data Flow Diagram (DFD) ระดับ Context และ Level 1
- ข้อมูลที่ sensitive และวิธี handle (encryption, masking)
- External data sources และ destinations
- Data transformation rules

**ประโยชน์:**
- Security Engineer ใช้ระบุจุดที่ข้อมูลอาจรั่วไหล
- Developer เข้าใจว่าต้อง validate/transform ข้อมูลที่ layer ไหน
- ช่วย compliance (PDPA, GDPR) — รู้ว่าข้อมูลส่วนตัวอยู่ที่ไหนบ้าง
- QA ออกแบบ test ตรวจสอบความถูกต้องของข้อมูล

**ใช้โดย:** Role 6 (Security), Role 4 (Dev), Role 7 (QA)

---

### `adr-log.md` — Architecture Decision Records

**ใช้ทำอะไร:**
บันทึกการตัดสินใจทางสถาปัตยกรรมที่สำคัญแต่ละรายการ พร้อม context, ตัวเลือกที่พิจารณา, เหตุผลที่เลือก, และผลที่ตามมา (ทั้งบวกและลบ)

**โครงสร้างหลัก:**
- ADR-NNN: [ชื่อการตัดสินใจ]
- Status: Proposed / Accepted / Deprecated / Superseded
- Context, Decision Drivers, Considered Options (pros/cons)
- Decision + Consequences + Follow-up Actions

**ประโยชน์:**
- ทีมรู้ว่า "ทำไมถึงเลือกแบบนี้" แม้เวลาผ่านไปนาน
- สมาชิกใหม่เข้าใจ history ของการออกแบบ
- ป้องกันการ revisit การตัดสินใจเดิมซ้ำๆ โดยไม่มีข้อมูลใหม่
- เมื่อ context เปลี่ยน สามารถ supersede ADR เก่าได้อย่างมีระเบียบ

**ใช้โดย:** ทีมพัฒนาทั้งหมด, Stakeholder

---

## 03-ux-ui/ — ออกแบบ UX/UI (5 ไฟล์)

> สร้างโดย **Role 3 — UX/UI Designer** ใน Phase 1

---

### `user-personas.md` — User Personas

**ใช้ทำอะไร:**
สร้างตัวแทนสมมติของผู้ใช้งานจริง พร้อม background, ความต้องการ, pain points, และพฤติกรรมการใช้งาน เพื่อให้ทีมออกแบบโดยคำนึงถึงคนจริง ไม่ใช่ assumption

**โครงสร้างหลัก:**
- แต่ละ Persona: ชื่อ, อายุ, อาชีพ, background
- Goals & Motivations
- Pain Points & Frustrations
- Technology Comfort Level
- Typical User Journey

**ประโยชน์:**
- Developer และ Designer ตัดสินใจ UX โดย "ถามตัวเอง ว่า Persona นี้จะทำยังไง"
- ลด bias จากความชอบส่วนตัวของทีม
- QA ใช้สร้าง test scenarios ที่สอดคล้องกับการใช้งานจริง
- สื่อสารกับ Stakeholder ได้ง่ายกว่าพูดถึง "user" แบบ abstract

**ใช้โดย:** Role 4 (Dev), Role 7 (QA), Stakeholder

---

### `journey-map.md` — User Journey Map

**ใช้ทำอะไร:**
แผนผังที่แสดงขั้นตอนทั้งหมดที่ผู้ใช้ทำเพื่อบรรลุเป้าหมาย ตั้งแต่ตระหนักถึงระบบ → ใช้งาน → บรรลุผล พร้อมความรู้สึก (positive/negative) และโอกาสปรับปรุง

**โครงสร้างหลัก:**
- Stages (Awareness, Discovery, Onboarding, Usage, Retention)
- Actions ใน stage นั้นๆ
- Thoughts & Emotions (frustrated, confused, delighted)
- Pain Points และ Opportunities

**ประโยชน์:**
- ระบุจุดที่ผู้ใช้ติดขัดหรือ drop off ได้ชัดเจน
- ช่วย prioritize feature ที่แก้ pain point จริงๆ
- ทีมเห็น "big picture" ของประสบการณ์ผู้ใช้
- ใช้ present กับ Stakeholder ให้เข้าใจ user experience

**ใช้โดย:** Role 1 (Requirement), Role 7 (QA)

---

### `wireframes.md` — Wireframes & Screen Flows

**ใช้ทำอะไร:**
โครงร่างหน้าจอแบบ low-fidelity แสดง layout, navigation flow, และ component placement — ก่อนออกแบบ visual จริง

**โครงสร้างหลัก:**
- Screen Inventory — รายการหน้าจอทั้งหมด
- Navigation Flow Diagram
- แต่ละหน้าจอ: ASCII wireframe หรือ description + key components
- Interaction notes (click → go to, validation behavior)

**ประโยชน์:**
- ทดสอบ logic การไหลของ UI ก่อนลงทุน design จริง
- Developer ใช้เป็น blueprint สร้าง component structure
- ได้ feedback จาก Stakeholder เร็ว ก่อนทำงานเยอะ
- QA ใช้วางแผน UI test cases

**ใช้โดย:** Role 4 (Dev), Role 7 (QA), Stakeholder

---

### `design-system.md` — Design System

**ใช้ทำอะไร:**
กำหนด visual language ที่ใช้ตลอดทั้งระบบ — สี, typography, spacing, component library rules เพื่อให้ UI มีความสม่ำเสมอ

**โครงสร้างหลัก:**
- Color Palette — Primary, Secondary, Semantic (success, error, warning)
- Typography — Font family, sizes, weights, line heights
- Spacing System — ระยะห่างมาตรฐาน (4px / 8px grid)
- Component Specs — Button, Input, Card, Modal, Table
- Accessibility Guidelines — contrast ratio, focus states

**ประโยชน์:**
- Developer ใช้ค่าจาก design system โดยตรง ไม่ต้องเดาเอง
- UI มีความสม่ำเสมอทุกหน้า
- เพิ่ม feature ใหม่ได้เร็วขึ้น เพราะใช้ component เดิม
- ผ่าน accessibility standards ได้ง่ายขึ้น

**ใช้โดย:** Role 4 (Dev), Role 7 (QA)

---

### `usability-testing.md` — Usability Testing Report

**ใช้ทำอะไร:**
บันทึกผลการทดสอบความสามารถในการใช้งานกับผู้ใช้จริงหรือ representative users พร้อม findings และ recommendations

**โครงสร้างหลัก:**
- Test Objectives & Methodology
- Participant Profiles
- Task Scenarios ที่ให้ทดสอบ
- Findings — Success Rate, Time on Task, Error Rate
- Usability Issues Severity Matrix
- Recommendations สำหรับแก้ไข

**ประโยชน์:**
- หลักฐานเชิงข้อมูลว่า UX ดีหรือไม่ดีตรงไหน
- Prioritize UX fixes ด้วย data ไม่ใช่ความเห็น
- Stakeholder เห็น ROI ของการลงทุน UX research
- ป้องกันปัญหา usability ก่อน launch จริง

**ใช้โดย:** Role 1 (Requirement), Role 10 (PM), Stakeholder

---

## 04-development/ — พัฒนาระบบ (4 ไฟล์)

> สร้างโดย **Role 4 — Software Developer** ใน Phase 2

---

### `code-structure.md` — โครงสร้างโค้ดและโมดูล

**ใช้ทำอะไร:**
บันทึก folder structure, module organization, naming conventions, และ dependency rules ที่ developer กำหนดไว้ อัปเดตทุก Sprint เมื่อมีโมดูลใหม่

**โครงสร้างหลัก:**
- Project Root Structure (directory tree)
- Module Breakdown — แต่ละโมดูล: controller, service, repository, model, tests
- Responsibilities ของแต่ละ layer
- Naming Conventions Table
- Module Dependencies (ห้าม Controller เรียก Repository โดยตรง เป็นต้น)
- Environment Variables ที่ใช้
- Sprint History — โมดูลที่เพิ่มแต่ละ Sprint

**ประโยชน์:**
- Code Reviewer เข้าใจโครงสร้างก่อน review ทำให้ review ได้ลึกขึ้น
- Developer ใหม่ onboard ได้เร็ว รู้ว่าไฟล์ไหนอยู่ที่ไหน
- ป้องกัน layering violations (เช่น business logic หลุดเข้า Controller)
- Security Engineer รู้จุดที่ต้อง review ด้านความปลอดภัย

**ใช้โดย:** Role 5 (Code Review), Role 6 (Security)

---

### `readme-template.md` — README ของโปรเจกต์

**ใช้ทำอะไร:**
โครงสร้าง README.md มาตรฐานสำหรับ repository จริงของโครงการ — ครอบคลุมทุกอย่างที่ developer ใหม่ต้องรู้เพื่อ setup และเริ่มพัฒนาได้

**โครงสร้างหลัก:**
- Project overview และ tech stack
- Prerequisites & Installation
- Environment setup (`.env` variables)
- How to run locally, run tests, build
- Project structure
- Contributing guidelines
- Deployment instructions

**ประโยชน์:**
- Developer ใหม่ setup environment ได้เองภายใน 30 นาที
- ลด "ถามเพื่อน" — ทุกอย่างอยู่ในไฟล์เดียว
- DevOps ใช้ reference สำหรับ CI/CD pipeline
- Onboarding time ลดลงอย่างมีนัยสำคัญ

**ใช้โดย:** Role 8 (DevOps), Role 9 (Tech Writer), Developer ใหม่

---

### `test-conventions.md` — มาตรฐานการเขียน Test

**ใช้ทำอะไร:**
กำหนด convention สำหรับการเขียน test ในโครงการ — naming pattern, folder structure, what to test, mock strategy, coverage requirements

**โครงสร้างหลัก:**
- Test Types ที่ใช้ (Unit, Integration, E2E)
- Naming Convention: `MethodName_Scenario_ExpectedResult`
- Folder/File structure สำหรับ test files
- Mock & Stub strategy (NSubstitute, Testcontainers)
- Coverage Requirements (≥80% สำหรับ Service/Domain)
- TDD Workflow ที่ใช้ในโครงการ
- ตัวอย่างโค้ด test จริง

**ประโยชน์:**
- ทีมเขียน test ในรูปแบบเดียวกัน อ่านแล้วเข้าใจได้เร็ว
- Code Reviewer ตรวจ test quality ได้ตาม standard เดียวกัน
- ลด debate ว่า "ควร test อะไร" — มี guideline ชัดเจน
- Coverage ไม่ตก เพราะทุกคนรู้ว่า layer ไหนต้อง test แน่ๆ

**ใช้โดย:** Role 5 (Code Review), Role 7 (QA)

---

### `pull-request-template.md` — PR Template

**ใช้ทำอะไร:**
โครงสร้างมาตรฐานสำหรับ Pull Request description — บังคับให้ developer อธิบาย context, การเปลี่ยนแปลง, วิธีทดสอบ, และ checklist ก่อน merge

**โครงสร้างหลัก:**
- Summary of Changes
- Related Issue/Story ID
- Type of Change (feature/bugfix/refactor/etc.)
- How to Test — ขั้นตอน reproduce หรือ verify
- Pre-merge Checklist (tests pass, coverage, docs updated, etc.)
- Screenshots (สำหรับ UI changes)

**ประโยชน์:**
- Code Reviewer ได้ข้อมูลครบก่อน review ไม่ต้องถามซ้ำ
- ลด back-and-forth ระหว่าง reviewer และ developer
- บังคับ developer ทบทวนงานตัวเองก่อน submit
- สร้าง audit trail ที่ดีของทุก change

**ใช้โดย:** Role 5 (Code Review)

---

## 05-code-review/ — ตรวจสอบโค้ด (2 ไฟล์)

> สร้างโดย **Role 5 — Code Reviewer** ใน Phase 2

---

### `review-checklist.md` — Checklist การตรวจสอบโค้ด

**ใช้ทำอะไร:**
รายการตรวจสอบที่ Code Reviewer ต้องผ่านทุกข้อก่อนอนุมัติ PR — ครอบคลุม code quality, security, testing, performance, และ documentation

**โครงสร้างหลัก:**
- Code Quality (naming, complexity, SOLID principles)
- Security (input validation, SQL injection, auth checks)
- Testing (coverage ≥80%, test quality, edge cases)
- Performance (N+1 queries, unnecessary loops, caching)
- Documentation (comments, API docs updated)
- Architecture (layering rules, no shortcuts)

**ประโยชน์:**
- Review คุณภาพสม่ำเสมอ ไม่ขึ้นกับว่า reviewer คนไหนทำ
- ไม่มี "ลืมตรวจ" เรื่องสำคัญ
- Developer รู้ล่วงหน้าว่าจะถูกตรวจอะไร → เขียนโค้ดได้ดีขึ้น
- ใช้ onboard reviewer ใหม่ได้ทันที

**ใช้โดย:** Role 4 (Dev) — เพื่อเตรียมตัว, Role 5 (Code Review)

---

### `review-report.md` — รายงานผล Code Review

**ใช้ทำอะไร:**
บันทึกผลการ review แต่ละ PR/Sprint — issues ที่พบ, severity, สถานะการแก้ไข, และ overall verdict

**โครงสร้างหลัก:**
- Review Summary (PR/Sprint, Reviewer, Date)
- Issues Found Table — ID, File, Severity, Description, Status
- Overall Assessment (Approved/Approved with conditions/Rejected)
- Positive Findings — สิ่งที่ทำได้ดี
- Recommendations สำหรับ Sprint ถัดไป

**ประโยชน์:**
- Tracking history ว่า issue ไหนถูกแก้แล้ว ยังค้างอยู่ไหน
- PM ใช้ monitor code quality trend ตลอดโครงการ
- Developer เรียนรู้จาก pattern ของ issues ที่พบซ้ำ
- เป็นหลักฐานว่า review ได้ทำจริง (audit trail)

**ใช้โดย:** Role 10 (PM), Role 4 (Dev)

---

## 06-security/ — ความปลอดภัย (5 ไฟล์)

> สร้างโดย **Role 6 — Security Engineer** ใน Phase 1 (review) และ Phase 2 (scan)

---

### `threat-model.md` — Threat Model (STRIDE)

**ใช้ทำอะไร:**
วิเคราะห์ภัยคุกคามที่อาจเกิดขึ้นกับระบบโดยใช้กรอบ STRIDE (Spoofing, Tampering, Repudiation, Information Disclosure, Denial of Service, Elevation of Privilege)

**โครงสร้างหลัก:**
- System Assets ที่ต้องปกป้อง
- Trust Boundaries และ Data Flow Diagram
- Threats Table — Threat, STRIDE category, Target, Likelihood, Impact
- Mitigation Controls สำหรับแต่ละ threat
- Residual Risk

**ประโยชน์:**
- ระบุช่องโหว่ด้านความปลอดภัยตั้งแต่ design phase (ถูกกว่าแก้หลัง deploy)
- Developer รู้ว่าต้อง implement security control อะไร
- เป็นพื้นฐานสำหรับ OWASP assessment และ security testing
- แสดงให้ compliance team เห็นว่ามีกระบวนการ security by design

**ใช้โดย:** Role 4 (Dev), Role 7 (QA), Compliance team

---

### `owasp-assessment.md` — OWASP Assessment

**ใช้ทำอะไร:**
ประเมินความปลอดภัยของระบบตาม OWASP Top 10 — ตรวจสอบทีละรายการว่าระบบมีมาตรการป้องกันครบหรือไม่

**โครงสร้างหลัก:**
- แต่ละ OWASP Top 10 category (A01-A10)
- Status: ✅ Mitigated / ⚠️ Partial / ❌ Not Addressed
- Evidence — หลักฐานว่า implement อะไรไปแล้ว
- Remaining Actions

**ประโยชน์:**
- Framework มาตรฐานสากลที่ Stakeholder และ auditor เชื่อถือ
- ตรวจสอบได้ครบทุก category ไม่ตกหล่น
- ใช้เป็น requirement สำหรับ penetration testing
- แสดงความพร้อมด้าน security ก่อน production launch

**ใช้โดย:** Role 4 (Dev), Auditor, Management

---

### `security-report.md` — รายงานผลการตรวจสอบความปลอดภัย

**ใช้ทำอะไร:**
สรุปผลการ security review/scan ทั้งหมด — vulnerabilities ที่พบ, severity, และแผนการแก้ไข

**โครงสร้างหลัก:**
- Executive Summary (สำหรับ management)
- Vulnerabilities Found Table — ID, Severity, CVSS Score, Description, Location
- Findings by Category
- Remediation Priority
- Sign-off section

**ประโยชน์:**
- Management เห็นภาพรวม risk ด้านความปลอดภัยในแบบที่เข้าใจง่าย
- Developer รู้ว่าต้องแก้อะไรก่อน (ตาม severity)
- Tracking history ของ security posture ตลอดโครงการ
- เอกสารสำหรับ compliance และ audit

**ใช้โดย:** Role 4 (Dev), Role 10 (PM), Management, Auditor

---

### `remediation-plan.md` — แผนแก้ไขช่องโหว่

**ใช้ทำอะไร:**
แผนปฏิบัติการแก้ไข vulnerabilities ทุกรายการ — owner, วิธีแก้, deadline, และสถานะ

**โครงสร้างหลัก:**
- Remediation Table — Vuln ID, Severity, Owner, Fix Description, Target Date, Status
- Critical/High items — แก้ภายใน Sprint นี้
- Medium items — แก้ใน Sprint ถัดไป
- Verification steps — วิธีตรวจสอบว่าแก้แล้วจริง

**ประโยชน์:**
- ไม่ปล่อยให้ vulnerability หลุดไปโดยไม่มีใครรับผิดชอบ
- PM ติดตาม security debt ได้เป็นระบบ
- ใช้ verify ในการ re-test หลังแก้ไข
- เป็น evidence สำหรับ compliance ว่ามีกระบวนการ remediation

**ใช้โดย:** Role 4 (Dev), Role 10 (PM)

---

### `security-policies.md` — นโยบายความปลอดภัย

**ใช้ทำอะไร:**
กำหนด security policies และ controls ที่ใช้ในโครงการนี้ — authentication policy, data handling, logging, incident response

**โครงสร้างหลัก:**
- Authentication & Authorization Policy (password rules, session timeout, MFA)
- Data Classification & Handling (sensitive data ต้อง encrypt, mask, etc.)
- Logging & Audit Trail Policy
- Incident Response Procedure
- Third-party / Dependency Policy

**ประโยชน์:**
- Developer รู้ว่าต้อง implement security อย่างไร ไม่ต้องเดา
- ลดความไม่สม่ำเสมอด้านความปลอดภัยระหว่าง developer
- ใช้ onboard developer ใหม่ด้านความปลอดภัย
- compliance และ audit — แสดงว่ามี policy จริง

**ใช้โดย:** Role 4 (Dev), Role 8 (DevOps)

---

## 07-qa-testing/ — ทดสอบคุณภาพ (5 ไฟล์)

> สร้างโดย **Role 7 — QA/Tester** ใน Phase 3

---

### `test-plan.md` — แผนการทดสอบ

**ใช้ทำอะไร:**
เอกสาร high-level ที่อธิบาย approach, scope, strategy, และ resources สำหรับการทดสอบทั้งโครงการหรือ Sprint

**โครงสร้างหลัก:**
- Test Objectives & Scope (ทดสอบอะไร ไม่ทดสอบอะไร)
- Test Strategy (Unit, Integration, E2E, Performance, Security)
- Test Environment & Tools
- Entry/Exit Criteria — เงื่อนไขเริ่ม/หยุดการทดสอบ
- Risk & Mitigation สำหรับ testing
- Schedule & Resources

**ประโยชน์:**
- ทุกคนเข้าใจ testing approach เดียวกัน
- PM ใช้ estimate effort และ timeline สำหรับ testing
- ป้องกัน "ลืมทดสอบ" cases สำคัญ
- เป็นเอกสารสำหรับ sign-off ว่า testing ครบถ้วน

**ใช้โดย:** Role 10 (PM), Stakeholder

---

### `test-cases.md` — Test Cases

**ใช้ทำอะไร:**
รายละเอียด test cases ทุก case — steps, expected result, actual result, pass/fail ครอบคลุมทั้ง happy path, edge cases, และ negative cases

**โครงสร้างหลัก:**
- Test Case ID, เชื่อมกับ Requirement ID (FR-XXX)
- Preconditions
- Test Steps (numbered)
- Expected Result
- Actual Result + Pass/Fail
- Priority (P0 Critical, P1 High, P2 Medium)

**ประโยชน์:**
- Reproducible testing — ใครทดสอบก็ได้ผลเหมือนกัน
- Traceability — รู้ว่าแต่ละ requirement ถูกทดสอบครบหรือไม่
- ใช้ regression testing เมื่อมีการเปลี่ยนแปลง
- หลักฐานว่าระบบทำงานถูกต้องตาม requirement

**ใช้โดย:** Developer (เพื่อเขียน unit test), Stakeholder (UAT)

---

### `bug-report.md` — รายงาน Bug

**ใช้ทำอะไร:**
บันทึก bugs ทุกรายการที่พบระหว่าง testing — รายละเอียดครบพอให้ developer reproduce และแก้ไขได้

**โครงสร้างหลัก:**
- Bug ID, Title, Severity (Critical/High/Medium/Low), Priority
- Steps to Reproduce (numbered, ชัดเจน)
- Expected vs Actual Behavior
- Environment & Version
- Screenshots/Logs
- Status (Open/In Progress/Fixed/Verified/Closed)

**ประโยชน์:**
- Developer แก้ bug ได้เร็วเพราะมีข้อมูลครบ ไม่ต้องถามกลับ
- Tracking progress การแก้ bug — รู้ว่ายังค้างเท่าไหร่
- PM ใช้ decide go/no-go สำหรับ release
- ป้องกัน bug กลับมาซ้ำ (เพราะมี record)

**ใช้โดย:** Role 4 (Dev), Role 10 (PM)

---

### `performance-test.md` — ผลการทดสอบ Performance

**ใช้ทำอะไร:**
บันทึกผลการทดสอบประสิทธิภาพระบบภายใต้ load ต่างๆ เปรียบเทียบกับ NFR targets ที่กำหนดไว้

**โครงสร้างหลัก:**
- Test Scenarios (normal load, peak load, stress test, spike test)
- Metrics ที่วัด — Response time (p50, p95, p99), Throughput, Error rate
- Results Table — Target vs Actual
- Bottlenecks ที่พบ
- Optimization Recommendations

**ประโยชน์:**
- ยืนยันว่าระบบรองรับ load จริงตาม NFR ที่ตกลงกับ Stakeholder
- ระบุ bottleneck ก่อน launch (database, CPU, memory, network)
- Baseline สำหรับ compare ใน release ถัดๆ ไป
- ช่วย capacity planning สำหรับ DevOps

**ใช้โดย:** Role 8 (DevOps), Role 2 (Architect), Stakeholder

---

### `qa-signoff.md` — QA Sign-off

**ใช้ทำอะไร:**
เอกสารยืนยันอย่างเป็นทางการว่า QA ได้ทดสอบครบ และ sign-off ว่าพร้อม release (หรือระบุ conditions ที่ต้องแก้ก่อน)

**โครงสร้างหลัก:**
- Test Summary — จำนวน test cases, pass/fail
- Critical Bugs Status — ต้องปิดทุก P0/P1 ก่อน sign-off
- Test Coverage Summary
- Outstanding Issues (ถ้ามี) และ risk acceptance
- Sign-off Signatures — QA Lead, PM, Stakeholder

**ประโยชน์:**
- Gate อย่างเป็นทางการก่อน deploy production
- ทุกฝ่ายรับรู้และยอมรับ quality ณ ขณะ release
- ป้องกันการ deploy โดยไม่ผ่าน testing
- เป็นหลักฐานทางกฎหมาย/compliance

**ใช้โดย:** Role 8 (DevOps), Role 10 (PM), Stakeholder

---

## 08-devops/ — DevOps & Deployment (6 ไฟล์)

> สร้างโดย **Role 8 — DevOps Engineer** ใน Phase 3

---

### `cicd-pipeline.md` — CI/CD Pipeline Configuration

**ใช้ทำอะไร:**
กำหนด pipeline ทั้งหมดตั้งแต่ push code ถึง deploy production — stages, tools, triggers, และ gates ที่ต้องผ่าน

**โครงสร้างหลัก:**
- Pipeline Stages — Build → Test → Security Scan → Deploy Staging → QA → Deploy Prod
- Tools ที่ใช้ (GitHub Actions, Azure DevOps, etc.)
- Trigger conditions (push to main, PR, tag)
- Quality Gates — test coverage, security scan pass
- Rollback procedure

**ประโยชน์:**
- Deploy ได้เร็วและ consistent ทุกครั้ง ไม่ผิดพลาดแบบ manual
- Quality gates ป้องกัน bad code เข้า production อัตโนมัติ
- Developer เห็น feedback เร็ว (fail fast)
- ลด human error ในการ deploy

**ใช้โดย:** Role 4 (Dev), Role 5 (Code Review)

---

### `docker-config.md` — Docker Configuration

**ใช้ทำอะไร:**
กำหนด Dockerfile, docker-compose, และ container configuration สำหรับ development, testing, และ production

**โครงสร้างหลัก:**
- Dockerfile (multi-stage build)
- docker-compose.yml สำหรับ local dev
- Environment variables handling
- Network configuration
- Volume mounts
- Health check configuration

**ประโยชน์:**
- "Works on my machine" problem หมดไป
- Developer setup local environment ได้ใน 1 คำสั่ง
- Production environment consistent กับ development
- ง่ายต่อ horizontal scaling

**ใช้โดย:** Role 4 (Dev), ทีม QA

---

### `environments.md` — Environment Configuration

**ใช้ทำอะไร:**
กำหนดรายละเอียดของแต่ละ environment (Dev, Staging, Production) — servers, configuration, access control, data policy

**โครงสร้างหลัก:**
- Environment Matrix — Dev / Staging / Prod
- แต่ละ environment: URL, server spec, database, external services
- Environment variables ที่ต่างกัน
- Access Control — ใครเข้าถึง environment ไหนได้
- Data Policy — prod data ห้ามใช้ใน dev

**ประโยชน์:**
- ทีมรู้ environment ทุกตัวชัดเจน ไม่สับสน
- ป้องกัน config ผิด environment (เช่น dev เชื่อม prod database)
- Security — access control ชัดเจน
- Onboarding — developer ใหม่รู้ว่าต้อง request access อะไร

**ใช้โดย:** Role 4 (Dev), Role 6 (Security), Role 7 (QA)

---

### `infrastructure.md` — Infrastructure as Code

**ใช้ทำอะไร:**
กำหนด infrastructure ทั้งหมด (cloud resources, networking, databases) ในรูปแบบ code — ใช้ Bicep (Azure) หรือ Terraform

**โครงสร้างหลัก:**
- Infrastructure overview (Cloud provider, regions)
- Resource list — VMs/Containers, Databases, Storage, CDN, Load Balancer
- Networking — VNet, Subnets, Security Groups
- Cost estimation
- IaC code references

**ประโยชน์:**
- Infrastructure reproducible — สร้างใหม่ได้ทุกเมื่อจาก code
- ป้องกัน "snowflake servers" ที่ไม่มีใครกล้าแตะ
- Disaster recovery ทำได้เร็ว
- Cost tracking และ optimization

**ใช้โดย:** Role 6 (Security), Management

---

### `monitoring.md` — Monitoring & Alerting

**ใช้ทำอะไร:**
กำหนด monitoring strategy, metrics ที่ track, dashboards, และ alert rules สำหรับ production system

**โครงสร้างหลัก:**
- Key Metrics — Application (error rate, latency), Infrastructure (CPU, memory, disk)
- Dashboards — ภาพรวมที่ต้อง monitor
- Alert Rules — threshold, severity, escalation path
- On-call procedure
- SLA monitoring

**ประโยชน์:**
- รู้ว่าระบบมีปัญหาก่อนที่ user จะ complain
- MTTR (Mean Time to Repair) ลดลง เพราะมี alert ชัดเจน
- ข้อมูล performance สำหรับ capacity planning
- SLA compliance — หลักฐานว่า uptime เป็นไปตามที่สัญญา

**ใช้โดย:** Role 10 (PM), Stakeholder

---

### `runbooks.md` — Runbooks (คู่มือปฏิบัติการ)

**ใช้ทำอะไร:**
คู่มือ step-by-step สำหรับ operations ที่ทำบ่อย หรือขั้นตอน incident response — เพื่อให้ทีม ops แก้ปัญหาได้รวดเร็วโดยไม่ต้องรอ expert

**โครงสร้างหลัก:**
- แต่ละ runbook: ชื่อ, trigger (เมื่อไหร่ใช้), prerequisites, steps, verification
- Deploy procedure
- Rollback procedure
- Database backup/restore
- Common incident playbooks (high CPU, DB connection exhausted, etc.)

**ประโยชน์:**
- On-call engineer แก้ปัญหาได้แม้ตอน 3 ทุ่ม ไม่ต้องโทรหาผู้เชี่ยวชาญ
- ลด MTTR อย่างมาก
- ป้องกัน human error ในขั้นตอนที่ sensitive
- Knowledge sharing — ลด single point of failure ในทีม

**ใช้โดย:** DevOps team, On-call engineers

---

## 09-documentation/ — เอกสารสำหรับผู้ใช้และนักพัฒนา (5 ไฟล์)

> สร้างโดย **Role 9 — Technical Writer** ตลอดกระบวนการ (Phase 3 เป็นหลัก)

---

### `user-manual.md` — คู่มือผู้ใช้งาน

**ใช้ทำอะไร:**
เอกสารอธิบายวิธีใช้งานระบบสำหรับ end user — เขียนในภาษาที่เข้าใจง่าย ไม่ใช้ศัพท์เทคนิค

**โครงสร้างหลัก:**
- Getting Started
- แต่ละฟีเจอร์หลัก: วิธีใช้ทีละขั้นตอน + screenshots
- Frequently Asked Questions
- Troubleshooting สำหรับปัญหาที่พบบ่อย
- Contact & Support

**ประโยชน์:**
- ลด support tickets — user แก้ปัญหาเองได้
- Onboarding user ใหม่เร็วขึ้น
- Training material สำหรับองค์กร
- User satisfaction สูงขึ้น เพราะใช้ระบบได้เต็มความสามารถ

**ใช้โดย:** End users, Support team

---

### `api-docs.md` — เอกสาร API สำหรับนักพัฒนา

**ใช้ทำอะไร:**
เอกสาร API ฉบับสมบูรณ์สำหรับ developer ที่ต้องการ integrate กับระบบ — มีตัวอย่าง request/response จริง

**โครงสร้างหลัก:**
- Authentication Guide (วิธีได้ token, วิธีใช้)
- แต่ละ endpoint — method, URL, parameters, request body, response, error codes
- Code examples (curl, Python, JavaScript, C#)
- Rate limiting & pagination
- Changelog

**ประโยชน์:**
- Third-party developer integrate ได้เองโดยไม่ต้องถามทีม
- ลด support burden สำหรับ API
- เพิ่มคุณค่าของ API เพราะ usability ดีขึ้น
- ใช้สร้าง SDK ในอนาคตได้

**ใช้โดย:** External developers, Integration partners

---

### `onboarding.md` — คู่มือ Onboarding สำหรับทีมพัฒนา

**ใช้ทำอะไร:**
คู่มือสำหรับ developer ใหม่ที่เพิ่งเข้าร่วมทีม — ตั้งแต่ setup environment จนถึง make first contribution ได้

**โครงสร้างหลัก:**
- Day 1 Checklist — accounts, access, tools
- Development Environment Setup
- Codebase Overview — architecture, key files, conventions
- First Contribution Guide
- Team processes — standup, PR process, deploy process
- Resources & contacts

**ประโยชน์:**
- Developer ใหม่ productive ได้เร็วขึ้นมาก (ลด onboarding time จากสัปดาห์ เป็นวัน)
- ลด interruptions ของ team members ที่ต้องตอบคำถาม
- Consistent setup — ไม่มีปัญหา "ของฉัน setup ต่างกัน"
- สะท้อน culture ของทีมที่ดูแลกัน

**ใช้โดย:** Developer ใหม่, HR

---

### `troubleshooting.md` — คู่มือแก้ปัญหา

**ใช้ทำอะไร:**
รวบรวมปัญหาที่พบบ่อย (Known Issues) พร้อม symptoms, สาเหตุ, และขั้นตอนแก้ไข — สำหรับทั้ง user และ developer

**โครงสร้างหลัก:**
- Common User Issues (login ไม่ได้, data ไม่แสดง, etc.)
- Common Developer Issues (environment setup, build errors)
- Error Code Reference
- Escalation Path — ถ้าแก้ไม่ได้ติดต่อใคร
- Diagnostic checklist

**ประโยชน์:**
- ลด support time — แก้ปัญหาที่พบบ่อยได้เอง
- Knowledge capture — ปัญหาที่เคยเจอไม่สูญหาย
- ลด MTTR สำหรับ incidents ที่เคยเกิดมาก่อน
- Support team ใช้เป็น first-line reference

**ใช้โดย:** Support team, Users, Developer

---

### `release-notes.md` — Release Notes

**ใช้ทำอะไร:**
สรุปการเปลี่ยนแปลงในแต่ละ version/release — features ใหม่, bug fixes, breaking changes, migration steps

**โครงสร้างหลัก:**
- Version, Release Date
- What's New — features ใหม่พร้อมอธิบาย
- Bug Fixes — issues ที่แก้แล้ว
- Breaking Changes — สิ่งที่ต้องแก้ถ้า upgrade
- Migration Guide (ถ้ามี)
- Known Issues — สิ่งที่ยังไม่แก้

**ประโยชน์:**
- User รู้ว่า version ใหม่มีอะไรเปลี่ยน
- Developer ที่ integrate รู้ว่ามี breaking change หรือไม่
- สร้าง transparency และ trust กับ users
- Reference สำหรับ rollback — รู้ว่า version ไหนมีอะไร

**ใช้โดย:** Users, Integration partners, Support team

---

## 10-project-management/ — บริหารโครงการ (5 ไฟล์)

> สร้างโดย **Role 10 — Product Owner/PM** ตลอดกระบวนการ

---

### `progress-dashboard.md` — Progress Dashboard ⭐ Single Source of Truth

**ใช้ทำอะไร:**
แดชบอร์ดกลางที่ track ความคืบหน้าของทั้งโครงการ — Phase, Role completion, Sprint progress, Deliverables, Decisions, และ Issues ทั้งหมดในที่เดียว

**โครงสร้างหลัก:**
- Project Overview (Overall Progress %, Current Phase, Current Role)
- Phase Progress (4 phases + status)
- Role Completion Table (10 roles)
- Sprint Progress (Phase 2)
- Deliverables Registry — ไฟล์ทุกไฟล์ที่สร้าง
- Key Decisions Log
- Issues & Blockers Log
- Activity Log (append-only)
- Definition of Done Checklist

**ประโยชน์:**
- ทุก Role ดู status ล่าสุดได้จากที่เดียว ไม่ต้องถามกันมาก
- ในโหมด Auto-Pipeline: AI อัปเดตอัตโนมัติทุกครั้งที่ Role เสร็จ
- PM เห็นภาพรวม ตัดสินใจได้เร็ว
- Stakeholder ขอ status update ได้ทันที
- Audit trail ครบ — ใครทำอะไร เมื่อไหร่

**ใช้โดย:** ทุก Role, Stakeholder, Management

---

### `roadmap.md` — Product Roadmap

**ใช้ทำอะไร:**
แผนระยะยาวของผลิตภัณฑ์ — features ที่จะทำแต่ละ Quarter/Phase พร้อม business objectives ที่เชื่อมโยง

**โครงสร้างหลัก:**
- Vision & Goals (12 เดือน)
- Roadmap Timeline — Q1/Q2/Q3/Q4
- Features ใน each quarter — Now / Next / Later
- Dependencies ระหว่าง features
- Milestones & Success Criteria

**ประโยชน์:**
- Stakeholder เห็นทิศทางระยะยาว ไม่ใช่แค่ sprint ปัจจุบัน
- ทีมเข้าใจว่ากำลังสร้างอะไรเพื่ออะไร
- ช่วย prioritize feature request ใหม่ — fit กับ roadmap ไหม
- Communication tool กับ management และ investor

**ใช้โดย:** Stakeholder, Management, ทีมพัฒนา

---

### `sprint-plan.md` — Sprint Plan

**ใช้ทำอะไร:**
รายละเอียดแผนการทำงานของแต่ละ Sprint — Stories ที่รับ, assignments, Definition of Done ของ Sprint นั้น

**โครงสร้างหลัก:**
- Sprint Goal (ภาพรวมว่า Sprint นี้จะสร้างอะไร)
- Sprint Backlog — Story ID, Description, Story Points, Assignee, Status
- Capacity — วัน/ชั่วโมงที่ทีมมี
- Dependencies (รอ Story อื่น หรือ API จากทีมอื่น)
- Sprint Definition of Done

**ประโยชน์:**
- ทีมรู้ชัดว่า Sprint นี้ต้องทำอะไร — ลด scope creep
- PM ติดตาม progress ระหว่าง Sprint ได้
- ใช้ใน Sprint Planning ceremony
- เป็น reference สำหรับ Sprint Review

**ใช้โดย:** Developer, Role 10 (PM)

---

### `sprint-retrospective.md` — Sprint Retrospective (ทุก Sprint รวมกัน)

**ใช้ทำอะไร:**
บันทึก retrospective ของทุก Sprint ไว้ในไฟล์เดียว — สะสม lessons learned ตลอดโครงการ พร้อมสรุปรวมตอนท้าย

**โครงสร้างหลัก:**
- แต่ละ Sprint: Metrics (planned vs actual), What Went Well, What to Improve, Action Items, Carry-over Stories
- Cumulative Lessons Learned (อัปเดตตอนท้ายโครงการ)
  - Process Insights
  - Technical Insights
  - Estimation Accuracy

**ประโยชน์:**
- ทีมเรียนรู้จาก Sprint ที่ผ่านมา ไม่ทำผิดซ้ำ
- PM ใช้ data (velocity, carry-over rate) วางแผน Sprint ถัดไปได้แม่นขึ้น
- Cumulative insights ใช้ในโครงการถัดไป
- สะท้อน culture ของ continuous improvement

**ใช้โดย:** ทีมพัฒนา, Role 10 (PM)

---

### `status-report.md` — Status Report

**ใช้ทำอะไร:**
รายงานความคืบหน้าของโครงการแบบ periodic (รายสัปดาห์/รายเดือน) สำหรับ Stakeholder และ Management ที่ไม่ได้อยู่ในทีม

**โครงสร้างหลัก:**
- Executive Summary (3-5 bullets)
- Overall Status (🟢 On Track / 🟡 At Risk / 🔴 Off Track)
- Progress ใน Period นี้
- Planned Next Period
- Risks & Issues (ที่ต้อง escalate)
- KPIs (ถ้า track)
- Decisions Needed จาก Stakeholder

**ประโยชน์:**
- Stakeholder ได้ข้อมูลสรุปที่อ่านง่าย ไม่ต้องเข้า standup
- PM บังคับตัวเองสรุปภาพรวมและระบุ blockers อย่างสม่ำเสมอ
- สร้าง accountability — ทุกคนรู้ว่า committed อะไร
- ใช้ escalate issues ได้อย่างเป็นทางการ

**ใช้โดย:** Stakeholder, Management, Executive

---

## สรุปภาพรวม

| โฟลเดอร์ | จำนวนไฟล์ | Phase หลัก | เขียนโดย |
|---------|----------|-----------|---------|
| 01-requirements | 4 | Phase 1 | Role 1 |
| 02-architecture | 6 | Phase 1 | Role 2 |
| 03-ux-ui | 5 | Phase 1 | Role 3 |
| 04-development | 4 | Phase 2 | Role 4 |
| 05-code-review | 2 | Phase 2 | Role 5 |
| 06-security | 5 | Phase 1+2 | Role 6 |
| 07-qa-testing | 5 | Phase 3 | Role 7 |
| 08-devops | 6 | Phase 3 | Role 8 |
| 09-documentation | 5 | Phase 3 | Role 9 |
| 10-project-management | 5 | ตลอดทั้งโครงการ | Role 10 |
| **รวม** | **47** | | |

---

## ไฟล์ที่สำคัญที่สุด (ต้องมีทุกโครงการ)

| ลำดับ | ไฟล์ | เหตุผล |
|------|------|-------|
| 1 | `progress-dashboard.md` | Single Source of Truth — ทุก Role ต้องอ่าน |
| 2 | `requirements-document.md` | Foundation ของทุกการตัดสินใจ |
| 3 | `architecture-diagram.md` | พิมพ์เขียวของทั้งระบบ |
| 4 | `tech-stack.md` | ทุกคนต้องรู้ว่าใช้อะไร |
| 5 | `api-spec.md` | Contract ระหว่าง Frontend/Backend/Client |
| 6 | `threat-model.md` | Security by design |
| 7 | `qa-signoff.md` | Gate ก่อน production |
