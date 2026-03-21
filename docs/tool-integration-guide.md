# Tool Integration Guide

**Version:** 1.0 | **Date:** 2026-03-21

---

## ภาพรวม

Template นี้ออกแบบให้ทำงานได้กับ tools จริงในกระบวนการพัฒนาซอฟต์แวร์
Guide นี้แสดงวิธี bridge ระหว่าง AI pipeline output กับ tools ที่ทีมใช้จริง

---

## 1. AI Agent / IDE Integration

Template รองรับ agent frameworks หลายตัว — เลือกตามที่ทีมใช้:

| Agent Framework | วิธีใช้ |
|----------------|--------|
| **Claude Code** | ใช้ได้ทันที — มี bash execution, file read/write ครบ |
| **Cursor** | เปิด project folder ใน Cursor, paste prompt จาก `.ai-prompts/` |
| **Windsurf** | เช่นเดียวกับ Cursor |
| **Devin / OpenHands** | ใช้กับ Auto-Pipeline โดยตรง — agent จะ execute code จริง |
| **Gemini + Google AI Studio** | Copy prompt + upload relevant files เป็น context |
| **ChatGPT (Projects)** | Upload template files เป็น knowledge base ใน Project |

### Agent Execution Mode (R4 & R7)

Role 4 (Developer) และ Role 7 (QA) มี `⚡ Agent Execution Mode` — เมื่อใช้กับ agent ที่มี shell access:

```bash
# R4: Agent จะรันคำสั่งเหล่านี้จริง
dotnet build          # .NET
dotnet test           # .NET
npm run build         # Node.js
npm test              # Node.js
python -m pytest      # Python
go test ./...         # Go

# R7: Agent จะรัน test tools จริง
npx playwright test
newman run collection.json
k6 run load-test.js
```

---

## 2. GitHub Integration

### 2.1 Branch Strategy

ใช้ Git Flow ที่สอดคล้องกับ Sprint-based development:

```
main                    ← Production branch (protected)
  └── develop           ← Integration branch
        ├── sprint/1-foundation     ← Sprint branch
        │     ├── feat/US-001-auth  ← Story branch
        │     └── feat/US-002-catalog
        ├── sprint/2-cart
        └── hotfix/...
```

### 2.2 Commit Convention

R4 (Developer) ใช้ Conventional Commits:

```
feat(auth): add JWT refresh token endpoint [US-001]
fix(cart): resolve negative quantity validation [US-005]
test(cart): add edge cases for checkout flow
docs(api): update cart endpoint documentation
refactor(product): extract search logic to service
chore(deps): upgrade axios to 1.7.0
```

### 2.3 PR Template

สร้างไฟล์ `.github/pull_request_template.md`:

```markdown
## Summary
[อธิบาย changes สั้นๆ]

## Related Stories
- Closes [US-XXX] — [ชื่อ Story]
- Closes [US-XXX] — [ชื่อ Story]

## Sprint
Sprint [N] — [ชื่อ Sprint]

## Type of Change
- [ ] feat: New feature
- [ ] fix: Bug fix
- [ ] refactor: Code refactor
- [ ] test: Tests only
- [ ] docs: Documentation only

## Testing
- [ ] Unit tests pass (coverage: [X]%)
- [ ] Integration tests pass
- [ ] Tested manually against ACs

## Checklist (ก่อน Request Review)
- [ ] ไม่มี hardcoded secrets
- [ ] ทุก endpoint มี input validation
- [ ] ไม่มี console.log / debug code หลงเหลือ
- [ ] Code follows coding-standards.md
```

### 2.4 GitHub Actions CI/CD

สอดคล้องกับ output ของ R8 (DevOps) — `templates/08-devops/cicd-pipeline.md`:

```yaml
# .github/workflows/ci.yml (ตัวอย่าง — R8 จะสร้างฉบับจริง)
name: CI Pipeline
on: [pull_request]
jobs:
  build-and-test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Build
        run: dotnet build
      - name: Test
        run: dotnet test --collect:"XPlat Code Coverage"
      - name: Coverage Gate (80%)
        run: |
          COVERAGE=$(cat coverage.xml | grep -oP 'line-rate="\K[^"]+')
          if (( $(echo "$COVERAGE < 0.8" | bc -l) )); then exit 1; fi
```

### 2.5 GitHub Issues จาก Pipeline

R7 (QA) Bug Reports → GitHub Issues:

```
Bug Title: [BUG] [Severity] ชื่อปัญหา — Sprint N
Labels: bug, P0/P1/P2, sprint-N
Assignee: Developer
Body: (ดู templates/07-qa-testing/bug-report.md)
```

---

## 3. Jira / Linear Integration

### 3.1 Mapping Sprint Plan → Tickets

หลัง Checkpoint 1 (Sprint Plan approved) → สร้าง tickets จาก `templates/10-project-management/sprint-plan.md`:

**Epic → Sprint:**
```
Epic: [ชื่อโปรเจกต์] v1.0
  └── Sprint 1: Foundation & Auth
  └── Sprint 2: Cart & Checkout
  └── Sprint N: ...
```

**Story → Ticket:**
```
Ticket ID: [US-001]
Title: User Registration
Points: [X] SP
Sprint: Sprint 1
Priority: Must Have
Description: (ดู user-story-map.md)
Acceptance Criteria: (copy จาก AC ใน user-story-map.md)
```

### 3.2 Status Mapping

| Pipeline Status | Jira Status | Linear Status |
|----------------|-------------|---------------|
| Story in Sprint Plan | To Do | Backlog |
| R4 implementing | In Progress | In Progress |
| R5 reviewing | In Review | In Review |
| R6 security scan | Security Review | In Review |
| Sprint completed | Done | Done |
| Carry over | Carry Over (custom) | Backlog (next sprint) |

### 3.3 Progress Dashboard → Jira Board

AI อัปเดต `progress-dashboard.md` อัตโนมัติ — ทีมควร sync ข้อมูลนี้กับ Jira เป็นระยะ:

```bash
# Script ตัวอย่าง (manual sync)
# อ่าน progress-dashboard.md → สร้าง/อัปเดต Jira tickets ผ่าน API
# ดู Jira REST API: /rest/api/3/issue
```

---

## 4. Figma Integration

### 4.1 จาก R3 Wireframes → Figma

output ของ R3 (`templates/03-ux-ui/wireframes.md`) คือ text-based wireframes
วิธีนำไป Figma:

**Option A: Manual** — Designer ใช้ wireframe.md เป็น spec แล้วสร้าง Figma frames เอง

**Option B: AI-assisted** — ใช้ prompt นี้กับ Figma AI:
```
จาก wireframe spec นี้ [paste section จาก wireframes.md]
สร้าง Figma frame ตาม design system:
- Primary: [hex]
- Font: [family]
- Components: [จาก design-system.md]
```

### 4.2 Design System → Figma Variables

`templates/03-ux-ui/design-system.md` Section Color Palette + Typography → Figma Variables:

```
Figma Variables:
  Color/Primary: #[hex]
  Color/Secondary: #[hex]
  Color/Error: #[hex]
  Typography/Base: [font-family] 16px/Regular
  Spacing/4: 4px
  Spacing/8: 8px
  ...
```

### 4.3 Figma → Developer Handoff

เมื่อ Designer สร้าง high-fidelity mockups ใน Figma แล้ว:
- Share Figma link ใน `templates/03-ux-ui/design-system.md` Section ท้าย
- R4 (Developer) ใช้ Figma Dev Mode หรือ Inspect panel
- CSS variables จาก Figma ควรตรงกับ design-system.md

---

## 5. Slack / Microsoft Teams Integration

### 5.1 Pipeline Notifications (Manual)

แต่ละ Checkpoint ควร post summary ใน project channel:

```
[Checkpoint 1 ✅] TechShop — Phase 1 Complete
• Requirements: 12 stories (8 Must | 3 Should | 1 Could)
• Architecture: Modular Monolith + .NET 10 + PostgreSQL
• Database: 8 tables designed
• UX/UI: 3 personas, 10 screens
• Sprint Plan: 3 Sprints approved

Sprint 1 starting: "Foundation & Auth"
Stories: US-001, US-002, US-003 (18 pts)
```

### 5.2 Sprint Review Notifications

```
[Sprint 1 Review ✅] TechShop
• Stories: 3/3 completed (18/18 pts)
• Coverage: 85%
• Code Review: APPROVED
• Security: PASSED

Sprint 2 starting: "Cart & Checkout"
```

---

## 6. Database Tools Integration

### 6.1 Migration Tools

R11 (DBA) สร้าง Migration Plan ใน `templates/11-dba/db-schema.md` Section 7
R4 (Developer) implement migrations จริงใช้ tool ตาม tech stack:

| Tech Stack | Migration Tool |
|-----------|---------------|
| .NET | Entity Framework Core Migrations (`dotnet ef migrations add`) |
| Node.js | Knex.js / Prisma Migrate |
| Python | Alembic (SQLAlchemy) |
| Go | golang-migrate / GORM AutoMigrate |

### 6.2 Schema Validation

ตรวจว่า code schema ตรงกับ `templates/11-dba/db-schema.md`:

```bash
# .NET: generate migration แล้วเทียบ
dotnet ef migrations script | diff - templates/11-dba/expected-schema.sql

# หรือใช้ database introspection tool เพื่อ compare
```

---

## 7. Testing Tools Integration

### 7.1 R7 QA Tools

| Test Type | Tool | Command |
|-----------|------|---------|
| E2E (Web) | Playwright | `npx playwright test` |
| E2E (Web) | Cypress | `npx cypress run` |
| API Testing | Newman (Postman) | `newman run collection.json` |
| Performance | k6 | `k6 run load-test.js` |
| Security Scan | OWASP ZAP | `zap-baseline.py -t http://localhost:3000` |

### 7.2 Coverage Reports

R5 (Code Reviewer) ต้องการ coverage >= 80%:

```bash
# .NET
dotnet test --collect:"XPlat Code Coverage"
reportgenerator -reports:coverage.xml -targetdir:coverage-report

# Node.js
npx vitest --coverage

# Python
pytest --cov=src --cov-report=html

# Go
go test ./... -coverprofile=coverage.out
go tool cover -html=coverage.out
```

---

## 8. Documentation Tools

### 8.1 R9 Output → Publishing

`templates/09-documentation/api-docs.md` → Swagger/OpenAPI UI:

```bash
# ถ้า R2 สร้าง api-spec.md ใน OpenAPI format
# Host ด้วย Swagger UI
npx swagger-ui-express

# หรือ Redoc
npx redoc-cli serve api-spec.yaml
```

### 8.2 User Manual Hosting

`templates/09-documentation/user-manual.md` → Notion / Confluence / GitBook:
- Copy markdown ไป Notion Pages หรือ Confluence
- หรือ publish เป็น static site ด้วย MkDocs / Docusaurus

---

## 9. Quick Start Checklist

เมื่อเริ่มโปรเจกต์ใหม่ ตั้งค่า integrations ตามลำดับ:

- [ ] สร้าง GitHub repository + ตั้ง branch protection สำหรับ `main`
- [ ] เพิ่ม `.github/pull_request_template.md`
- [ ] สร้าง GitHub Actions workflow (ดู R8 output สำหรับ full config)
- [ ] สร้าง Jira/Linear project + import Sprint Plan หลัง Checkpoint 1
- [ ] Share Figma link ใน design-system.md หลัง R3 เสร็จ
- [ ] ตั้ง Slack/Teams channel สำหรับ project notifications
- [ ] ตรวจสอบว่า database migration tool ตรงกับ tech stack ที่เลือก
