# Workflow Orchestration

## Software Development Lifecycle (SDLC) Process

---

## Workflow Diagram

```
┌─────────────────────────────────────────────────────────────────────┐
│                        PRODUCT OWNER (10)                           │
│                    Orchestrates & Prioritizes                       │
└────────┬──────────────────────────────────────────────────┬─────────┘
         │                                                  │
         ▼                                                  │
┌─────────────────┐                                         │
│ 1. REQUIREMENT  │  Requirements Document                  │
│    ANALYST      │  User Stories                           │
│                 │  Priority Matrix                        │
└────────┬────────┘                                         │
         │                                                  │
         ▼                                                  │
┌─────────────────┐     ┌──────────────────┐               │
│ 2. SYSTEM       │────→│ 6. SECURITY      │ (Architecture │
│    ARCHITECT    │     │    ENGINEER      │  Review)       │
│                 │     │                  │               │
└────────┬────────┘     └──────────────────┘               │
         │                                                  │
    ┌────┴────┐                                            │
    ▼         ▼                                            │
┌────────┐ ┌──────────────┐                                │
│ 3. UX/ │ │ Architecture │                                │
│ UI     │ │ Documents    │                                │
└───┬────┘ └──────────────┘                                │
    │                                                      │
    ▼                                                      │
┌─────────────────┐                                        │
│ 4. SOFTWARE     │  Source Code                           │
│    DEVELOPER    │  Tests                                 │
│                 │  Pull Request                          │
└────────┬────────┘                                        │
         │                                                  │
         ▼                                                  │
┌─────────────────┐                                        │
│ 5. CODE         │──→ Request Changes? ──→ Back to Dev    │
│    REVIEWER     │                                        │
│                 │──→ Approved                            │
└────────┬────────┘                                        │
         │                                                  │
         ▼                                                  │
┌─────────────────┐                                        │
│ 6. SECURITY     │──→ Critical/High? ──→ Back to Dev      │
│    ENGINEER     │                                        │
│    (Scan)       │──→ Pass                                │
└────────┬────────┘                                        │
         │                                                  │
         ▼                                                  │
┌─────────────────┐                                        │
│ 7. QA / TESTER  │──→ Bugs found? ──→ Back to Dev        │
│                 │                                        │
│                 │──→ QA Sign-off                         │
└────────┬────────┘                                        │
         │                                                  │
         ▼                                                  │
┌─────────────────┐                                        │
│ 8. DEVOPS       │  Deploy to Production                  │
│    ENGINEER     │  Monitoring Active                     │
└────────┬────────┘                                        │
         │                                                  │
         ▼                                                  │
┌─────────────────┐                                        │
│ 9. TECHNICAL    │  Documentation Updated                 │
│    WRITER       │  (Continuous throughout)                │
└────────┬────────┘                                        │
         │                                                  │
         ▼                                                  │
    ┌────────────┐                                         │
    │  RELEASE   │◄────────────────────────────────────────┘
    │  COMPLETE  │
    └────────────┘
```

## Phase Details

### Phase 1: Requirements & Planning

| Step | Actor | Input | Output | Gate |
|------|-------|-------|--------|------|
| 1.1 | PO + Stakeholders | Business needs | Project brief | Stakeholder approval |
| 1.2 | Requirement Analyst | Project brief | Requirements doc | PO review |
| 1.3 | Requirement Analyst | Requirements | User stories + priority | PO approval |
| 1.4 | PO | Approved requirements | Sprint plan | Team commitment |

### Phase 2: Design

| Step | Actor | Input | Output | Gate |
|------|-------|-------|--------|------|
| 2.1 | System Architect | Requirements | Architecture doc | Design review |
| 2.2 | System Architect | Architecture | Tech stack + API spec | Team approval |
| 2.3 | Security Engineer | Architecture | Security review | No critical issues |
| 2.4 | UX/UI Designer | Requirements + Architecture | UI designs | Design review |

### Phase 3: Development

| Step | Actor | Input | Output | Gate |
|------|-------|-------|--------|------|
| 3.1 | Developer | Design docs | Source code + tests | Self-review |
| 3.2 | Developer | Code complete | Pull request | Tests passing |
| 3.3 | Code Reviewer | Pull request | Review feedback | Approval |
| 3.4 | Security Engineer | Code | Security scan | No Critical/High |

### Phase 4: Quality Assurance

| Step | Actor | Input | Output | Gate |
|------|-------|-------|--------|------|
| 4.1 | QA | Features | Test plan + cases | Coverage adequate |
| 4.2 | QA | Deployed to QA env | Test results | All P0/P1 pass |
| 4.3 | QA | Test results | Bug reports | Bugs triaged |
| 4.4 | QA | All retesting done | QA sign-off | Sign-off obtained |

### Phase 5: Deployment

| Step | Actor | Input | Output | Gate |
|------|-------|-------|--------|------|
| 5.1 | DevOps | QA sign-off | Staging deploy | Smoke tests pass |
| 5.2 | PO | Staging validation | Go/No-go decision | Approval |
| 5.3 | DevOps | Approval | Production deploy | Health checks pass |
| 5.4 | DevOps | Production live | Monitoring active | No alerts |

### Phase 6: Post-Release

| Step | Actor | Input | Output |
|------|-------|-------|--------|
| 6.1 | Technical Writer | All docs | Updated documentation |
| 6.2 | PO | Release complete | Release communication |
| 6.3 | Team | Release | Retrospective + lessons learned |

---

## Definition of Done Checklist

### Per Story
- [ ] Acceptance criteria met
- [ ] Code reviewed and approved
- [ ] Unit tests written (>= 80% coverage)
- [ ] No Critical/High bugs
- [ ] Documentation updated

### Per Sprint
- [ ] All committed stories Done
- [ ] Sprint demo completed
- [ ] Retrospective conducted
- [ ] Backlog groomed for next sprint

### Per Release
- [ ] Requirements approved by Stakeholder
- [ ] Design Review passed
- [ ] Code passed Code Review and Security Scan
- [ ] Unit Test Coverage >= 80%
- [ ] QA Testing passed all critical test cases
- [ ] Security Assessment: no Critical/High vulnerabilities
- [ ] Documentation complete
- [ ] Deployed to Production successfully
- [ ] Monitoring & Alerting operational
- [ ] Release notes published
- [ ] Stakeholders notified

---

## Role Interaction Matrix

| From \ To | Req | Arch | UX | Dev | Review | Sec | QA | DevOps | Doc | PO |
|-----------|-----|------|----|-----|--------|-----|-----|--------|-----|-----|
| **Req** | - | Specs | Specs | - | - | - | - | - | Req doc | Report |
| **Arch** | Questions | - | Constraints | Tech spec | - | Review | - | Infra req | Arch doc | Report |
| **UX** | Questions | Questions | - | Designs | - | - | Flows | - | UI doc | Report |
| **Dev** | Questions | Questions | Questions | - | PR | - | Builds | Deploy req | Code doc | Report |
| **Review** | - | - | - | Feedback | - | - | - | - | - | Report |
| **Sec** | - | Feedback | - | Vulns | - | - | - | Sec config | Sec doc | Report |
| **QA** | Verify AC | - | Verify UX | Bugs | - | - | - | Env req | Test doc | Report |
| **DevOps** | - | - | - | - | - | - | Env ready | - | Ops doc | Report |
| **Doc** | Review | Review | Review | Review | - | Review | Review | Review | - | Report |
| **PO** | Priority | Decisions | Approval | Priority | - | Risk | Sign-off | Approval | Review | - |

---

## Progress Dashboard (Single Source of Truth)

ไฟล์ `templates/10-project-management/progress-dashboard.md` ทำหน้าที่เป็น **shared state** ระหว่างทุก Role

- ในโหมด **Auto-Pipeline**: AI จะสร้างและอัปเดตอัตโนมัติหลังจาก Role เสร็จงาน, Sprint เสร็จ, Checkpoint ผ่าน
- ในโหมด **Manual**: ผู้ใช้ควรอัปเดตเองหลังจากแต่ละ Role ทำงานเสร็จ

**สิ่งที่ติดตาม:**
- Phase Progress (4 phases)
- Role Completion (10 roles)
- Sprint Progress (Phase 2)
- Deliverables Registry (ไฟล์ทั้งหมดที่สร้าง)
- Key Decisions, Issues & Blockers, Activity Log
- Definition of Done checklist

**สูตรคำนวณ Overall Progress:**
Phase 1 = 25% | Phase 2 = 40% | Phase 3 = 25% | Phase 4 = 10%
