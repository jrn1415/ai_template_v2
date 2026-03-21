# AI Code Template - Software Development Team Simulation

> **ภาษาไทย**: อ่าน [`README-th.md`](README-th.md) สำหรับเวอร์ชันภาษาไทย

Central template for simulating a complete software development team with 11 specialized roles, designed to work with AI coding assistants (Claude, ChatGPT, etc.) or as a standalone SDLC framework.

## What's Inside

### AI Prompts (`.ai-prompts/`)

| # | Role | Purpose |
|---|------|---------|
| 01 | Requirement Analyst | Gather & prioritize requirements, create user stories |
| 02 | System Architect | Design architecture, choose tech stack, define APIs |
| 11 | Database Administrator (DBA) | Design DB Schema, indexing, performance, migrations |
| 03 | UX/UI Designer | Create personas, wireframes, design system |
| 04 | Software Developer | Write clean code, tests, documentation |
| 05 | Code Reviewer | Review code quality, security, performance |
| 06 | Security Engineer | Threat modeling, OWASP assessment, security policies |
| 07 | QA/Tester | Test planning, execution, bug reporting |
| 08 | DevOps/CICD | CI/CD pipeline, infrastructure, monitoring |
| 09 | Technical Writer | User docs, API docs, onboarding guides |
| 10 | Product Owner/PM | Sprint planning, tracking, stakeholder communication |

### Deliverable Templates (`templates/`)

43 ready-to-use templates covering every phase of software development:

- **Requirements**: Requirements doc (incl. MoSCoW matrix), user story map, risk analysis
- **Architecture**: Architecture diagram, tech stack, API spec, data flow, ADR log
- **Database**: DB schema, table definitions, indexing strategy, migration plan
- **UX/UI**: User personas, journey map, wireframes, design system
- **Development**: README template, code structure guide, PR template
- **Code Review**: Review report (incl. review checklist)
- **Security**: Architecture review, threat model (STRIDE), OWASP assessment, security report, remediation plan, policies
- **QA Testing**: Test plan, test cases, bug report, performance test, QA sign-off
- **DevOps**: CI/CD pipeline, Docker config, monitoring, runbooks, environments, infrastructure
- **Documentation**: User manual, API docs, onboarding, troubleshooting, release notes
- **Project Management**: Roadmap, sprint plan, sprint retrospective, **progress dashboard**

## Quick Start

### Auto-Pipeline (Recommended — Easiest)

1. Fill in `requirement_template.md` with your project details
2. Tell Claude: `"Start development using auto-pipeline from requirement_template.md"`
3. Claude will automatically run all 11 roles with Sprint-based development and checkpoints for your review

```
Fill in requirement_template.md
        ↓
AI validates + asks follow-up questions (if needed)
        ↓
Phase 1: Requirements → Architecture → DBA → Security Review → UX/UI → Sprint Planning
        ↓ ⏸️ Checkpoint 1 (review & approve + review Sprint Plan)
Phase 2: Sprint-based Development (one Sprint at a time)
        ├─ Sprint N: Development → Code Review → Security
        ↓ ⏸️ Sprint Review (review deliverables per Sprint)
        └─ Repeat until all Sprints complete
        ↓ ⏸️ Checkpoint 2 (review overall)
Phase 3: QA Testing → DevOps → Documentation
        ↓ ⏸️ Checkpoint 3 (review & approve)
Phase 4: Project Summary → Final Delivery (with Sprint-by-Sprint breakdown)
```

### Manual Mode

1. Fill in `CLAUDE.md` with your project details
2. Copy the AI prompt from `.ai-prompts/[role]/prompt.md`
3. Replace `[placeholders]` with your specifics
4. Use output templates from `templates/` to structure results
5. Follow the workflow defined in `docs/workflow.md`

## Workflow

```
Requirements --> Architecture --> DBA --> Security Review --> UX/UI --> Sprint Planning
                                                                          |
                                                                   Sprint-based Development
                                                                   ├─ Sprint N: Dev → Code Review → Security Scan
                                                                   └─ Sprint Review per Sprint
                                                                          |
                                                                   QA Testing
                     |
               DevOps Deploy --> Production
                     |
            Documentation (continuous)
            Product Owner (orchestrates all)
```

## Structure

```
.
├── CLAUDE.md                    # Project configuration
├── requirement_template.md      # Fill this to start Auto-Pipeline
├── .ai-prompts/                 # 11 role-based AI prompts + Auto-Pipeline
│   ├── auto-pipeline-prompt.md  # Master prompt (runs all roles)
│   ├── 01-requirements/
│   ├── 02-architecture/
│   ├── ...
│   ├── 10-project-management/
│   └── 11-dba/
├── templates/                   # 43 deliverable templates
│   ├── 01-requirements/
│   ├── 02-architecture/
│   ├── 03-ux-ui/
│   ├── 04-development/
│   ├── 05-code-review/
│   ├── 06-security/
│   ├── 07-qa-testing/
│   ├── 08-devops/
│   ├── 09-documentation/
│   ├── ...
│   ├── 10-project-management/
│   └── 11-dba/
├── standards/                   # Company-wide baseline standards
│   ├── coding-standards.md      # Naming, TDD, Git, Security baseline
│   └── tech-stack-catalog.md    # Approved tech stack catalog
├── docs/
│   ├── workflow.md              # SDLC workflow & DoD
│   ├── how-to-use-en.md        # Usage guide (English)
│   ├── how-to-use-th.md        # Usage guide (Thai)
│   ├── templates-guide.md      # Detailed guide to all templates
│   ├── context-management.md   # Context window management & session resume
│   ├── rejection-handling.md   # Iteration & rejection handling protocol
│   ├── tool-integration-guide.md  # GitHub, Jira, Figma, CI/CD integration
│   ├── model-selection-guide.md   # AI model selection per role
│   └── improvement-recommendations.md  # Change log & recommendations
├── examples/
│   └── techshop/               # Complete TechShop reference project outputs
├── README.md                    # Project overview (English)
└── README-th.md                 # Project overview (Thai)
```

## Usage Modes

| Mode | Description |
|------|-------------|
| **Auto-Pipeline** | Fill requirement template → AI runs all roles automatically with Sprint-based development & checkpoints |
| **Full Simulation** | Run all 11 roles sequentially with manual control |
| **Single Role** | Use one role's prompt for specific needs |
| **Template Only** | Use deliverable templates without AI prompts |
| **Hybrid** | Combine AI prompts with manual team processes |
