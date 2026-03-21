# AI Model Selection Guide

**Version:** 1.0 | **Date:** 2026-03-21

---

## ภาพรวม

Template นี้รองรับ AI หลายตัว (Claude, Gemini, GPT-4) เลือก model ที่เหมาะกับแต่ละ Role
เพื่อ balance ระหว่าง quality, cost, และ speed

---

## 1. Role-by-Role Recommendations

### Primary Stack: Google Gemini Enterprise

> บริษัทที่ใช้ Gemini Enterprise ใช้ตารางนี้เป็น baseline

| Role | งาน | Model แนะนำ | เหตุผล |
|------|-----|-------------|--------|
| R1 — Requirements | วิเคราะห์ความต้องการ, สร้าง User Stories | Gemini [latest Pro model] | Reasoning + Analysis ลึก |
| R2 — Architecture | ออกแบบ system, เลือก tech stack | Gemini [latest Pro model] | Reasoning complex tradeoffs |
| R11 — DBA | ออกแบบ DB schema, normalization | Gemini [latest Pro model] | SQL knowledge + data modeling |
| R3 — UX/UI | Personas, wireframes, design system | Gemini [latest Pro model] | Multimodal + creative output |
| R4 — Developer | เขียนโค้ด, TDD, migrations | Gemini [latest Pro model] | Code generation + long context |
| R5 — Code Review | Review SOLID, security, performance | Gemini [latest Pro model] | Code analysis ลึก |
| R6 — Security | STRIDE, OWASP, penetration insights | Gemini [latest Pro model] | Security domain knowledge |
| R7 — QA | Test cases, bug triage, E2E testing | Gemini [latest Pro model] | Analysis + agent execution |
| R8 — DevOps | CI/CD config, infrastructure | Gemini [latest Pro model] | Config generation + infra knowledge |
| R9 — Tech Writer | Documentation, API docs, onboarding | Gemini [latest Pro model] | Structured writing + synthesis |
| R10 — PM | Project summary, lessons learned | Gemini [latest Pro model] | Synthesis จากทุก Role |

---

### Alternative Stack: Anthropic Claude

| Role | งาน | Model แนะนำ | หมายเหตุ |
|------|-----|-------------|---------|
| R1 — Requirements | วิเคราะห์ความต้องการ | Claude Sonnet 4.6 | ดีมากสำหรับ structured analysis |
| R2 — Architecture | System design ซับซ้อน | Claude Opus 4.6 | Reasoning ระดับสูงสุด |
| R11 — DBA | DB schema + normalization | Claude Sonnet 4.6 | SQL + data modeling ดี |
| R3 — UX/UI | Personas + wireframes | Claude Sonnet 4.6 | Creative + structured |
| R4 — Developer | Code generation (โปรเจกต์ใหญ่) | Claude Sonnet 4.6 | Code quality ดีมาก, cost-effective |
| R4 — Developer | Code generation (โปรเจกต์เล็ก) | Claude Haiku 4.5 | เร็ว + ประหยัด |
| R5 — Code Review | Code analysis | Claude Sonnet 4.6 | Code review แม่นยำ |
| R6 — Security | OWASP/STRIDE + code review | Claude Opus 4.6 | Security reasoning ลึก |
| R7 — QA | Test planning + execution | Claude Sonnet 4.6 | Agent execution ดี (Claude Code) |
| R8 — DevOps | CI/CD + infrastructure | Claude Sonnet 4.6 | Config + infra knowledge ดี |
| R9 — Tech Writer | Documentation | Claude Sonnet 4.6 | Writing quality สูง |
| R10 — PM | Summary + synthesis | Claude Sonnet 4.6 | Synthesis + structured output |

---

### Alternative Stack: OpenAI GPT-4

| Role | Model แนะนำ | หมายเหตุ |
|------|-------------|---------|
| R1, R2, R6 | GPT-4o | Complex reasoning roles |
| R4, R5, R8 | GPT-4o | Code-heavy roles |
| R3, R9 | GPT-4o | Creative + writing roles |
| R7 | GPT-4o + Codex | Testing + code execution |
| R10 | GPT-4o | Synthesis role |

---

## 2. Task-Type Matrix

เลือก model ตามลักษณะงานหลัก:

| ลักษณะงาน | ต้องการ | เหมาะกับ |
|-----------|--------|---------|
| Complex reasoning + tradeoffs | Strong reasoning | Gemini Pro / Claude Opus / GPT-4o |
| Code generation (ยาว) | Long context + code quality | Gemini Pro / Claude Sonnet / GPT-4o |
| Code generation (สั้น/ซ้ำๆ) | Speed + cost | Claude Haiku / Gemini Flash |
| Document writing | Writing quality | Claude Sonnet / Gemini Pro |
| Security analysis | Security domain knowledge | Claude Opus / Gemini Pro |
| Agent execution (shell) | Tool use + agentic | Claude (Claude Code) / Gemini (ADK) |
| Multimodal (อ่านรูป wireframe) | Vision capability | Gemini Pro / GPT-4o / Claude Sonnet |

---

## 3. Context Window Requirements

แต่ละ Role มีความต้องการ context window ต่างกัน:

| Role | Context ที่อ่าน | Minimum Window |
|------|---------------|----------------|
| R1 | requirement_template.md | 32K |
| R2 | R1 outputs (3 files) | 64K |
| R11 | R1+R2 outputs | 64K |
| R3 | R1+R2 outputs | 64K |
| R4 | R1+R2+R11+R3 outputs + existing code | 128K+ |
| R5 | Source code (all sprint files) | 128K+ |
| R6 | Architecture + source code | 128K+ |
| R7 | Requirements + all outputs | 128K+ |
| R8 | Architecture + R7 | 64K |
| R9 | All outputs (synthesis) | 128K+ |
| R10 | progress-dashboard + all summaries | 64K |

> **ข้อควรระวัง:** ถ้า model มี context window เล็กกว่าที่ระบุ → ใช้ Session Resume Protocol (ดู `docs/context-management.md`)

---

## 4. Cost Optimization Guide

### โปรเจกต์เล็ก (< 5 Must Have features)

```
Phase 1: ใช้ Sonnet/Pro ทุก Role
Phase 2: ใช้ Haiku/Flash สำหรับ boilerplate code (R4)
         ใช้ Sonnet/Pro สำหรับ logic ซับซ้อน
Phase 3: ใช้ Sonnet/Pro ทุก Role
```

### โปรเจกต์กลาง (5-15 Must Have features)

```
Phase 1: ใช้ Opus/Pro สำหรับ R2 (Architecture) + R6 Phase 1
         ใช้ Sonnet/Pro สำหรับ Role อื่น
Phase 2: ใช้ Sonnet สำหรับ R4 (Developer) — ทำงานหลายรอบ
         ใช้ Sonnet สำหรับ R5, R6
Phase 3: ใช้ Sonnet/Pro
```

### โปรเจกต์ใหญ่ (> 15 Must Have features)

```
ทุก Role: ใช้ model ที่แรงที่สุด (Opus / Gemini Pro)
เพราะ consistency และ quality สำคัญกว่า cost ในโปรเจกต์ขนาดนี้
```

---

## 5. Model Capabilities Reference (2026)

### Anthropic Claude

| Model | Context | Code | Reasoning | Speed | Cost |
|-------|---------|------|-----------|-------|------|
| Claude Opus 4.6 | 200K | ★★★★★ | ★★★★★ | ช้า | สูงสุด |
| Claude Sonnet 4.6 | 200K | ★★★★★ | ★★★★☆ | กลาง | กลาง |
| Claude Haiku 4.5 | 200K | ★★★☆☆ | ★★★☆☆ | เร็วมาก | ต่ำสุด |

### Google Gemini

| Model | Context | Code | Reasoning | Speed | Cost |
|-------|---------|------|-----------|-------|------|
| Gemini [latest Pro model] | 1M+ | ★★★★★ | ★★★★★ | กลาง | กลาง-สูง |
| Gemini Flash | 1M | ★★★★☆ | ★★★☆☆ | เร็วมาก | ต่ำ |

### OpenAI

| Model | Context | Code | Reasoning | Speed | Cost |
|-------|---------|------|-----------|-------|------|
| GPT-4o | 128K | ★★★★★ | ★★★★☆ | กลาง | กลาง |
| GPT-4o mini | 128K | ★★★☆☆ | ★★★☆☆ | เร็ว | ต่ำ |

---

## 6. Special Considerations

### Agent Execution Mode (R4, R7)

เมื่อ Role ต้อง execute code จริง ต้องใช้ AI ที่มี tool use capability:

| Agent | AI ที่รองรับ |
|-------|------------|
| Claude Code | Claude (Sonnet/Opus) |
| Cursor / Windsurf | Claude / GPT-4o |
| Devin | GPT-4 based |
| OpenHands | หลาย models |
| Gemini ADK | Gemini |

### Multimodal Roles (R3 UX/UI)

ถ้าต้องการให้ AI อ่าน existing design files หรือ screenshots:
- Claude Sonnet 4.6+ รองรับ vision
- Gemini Pro รองรับ vision
- GPT-4o รองรับ vision

### Long Context Roles (R4, R5, R6 — Sprint ใหญ่)

ถ้า codebase ใหญ่และต้อง review ทั้งหมด:
- Gemini Pro (1M context) ดีสุด
- Claude Sonnet (200K) ใช้ร่วมกับ context chunking
- ดู `docs/context-management.md` สำหรับ chunking strategy

---

## 7. Prompt ระบุ Model ใน Auto-Pipeline

เมื่อใช้ Auto-Pipeline กับ model ที่ต้องการ ระบุใน prompt แรก:

```
เริ่มพัฒนาตาม auto-pipeline จาก requirement_template.md

Model: Claude Sonnet 4.6 (ใช้ตลอด pipeline)
Agent: Claude Code (มี shell execution)
```

หรือ ถ้าต้องการ mixed:

```
เริ่มพัฒนาตาม auto-pipeline จาก requirement_template.md

Model Strategy:
- R2 (Architecture), R6 (Security): ใช้ Claude Opus (complex reasoning)
- R4 (Developer), R5 (Code Review): ใช้ Claude Sonnet (code quality)
- R1, R3, R7, R8, R9, R10: ใช้ Claude Sonnet (balanced)
```
