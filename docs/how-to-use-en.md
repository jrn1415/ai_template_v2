# How to Use This Template

## Quick Start Guide

---

## Step 1: Initialize Your Project

1. Clone or copy this template repository
2. Open `CLAUDE.md` and fill in your project information:
   - **System Name** - e.g., "Inventory Management System"
   - **Business Goal** - e.g., "Reduce inventory processing time by 50%"
   - **Primary Users** - e.g., "Warehouse staff, Managers"
   - **Constraints** - e.g., "Must support 1,000 concurrent users"

## Step 2: Follow the Workflow

### Order of Operations

```
 1. Requirements Analysis  →  Fill templates/01-requirements/
 2. System Architecture    →  Fill templates/02-architecture/
 3. UX/UI Design           →  Fill templates/03-ux-ui/
 4. Development            →  Use  templates/04-development/
 5. Code Review            →  Use  templates/05-code-review/
 6. Security Assessment    →  Use  templates/06-security/
 7. QA Testing             →  Use  templates/07-qa-testing/
 8. DevOps & Deployment    →  Use  templates/08-devops/
 9. Documentation          →  Use  templates/09-documentation/
10. Project Management     →  Use  templates/10-project-management/
```

> **Note**: You don't have to complete every step. Pick only the ones relevant to your needs.

---

## Step 3: Use with AI (Claude / ChatGPT / Others)

### Option A: Full Team Simulation (Recommended for new projects)

1. Copy the prompt from `.ai-prompts/[role]/prompt.md`
2. Paste it into your AI tool
3. Replace all `[placeholders]` with your actual project details
4. The AI will generate deliverables based on the template structure

**Example**:
```
1. Open .ai-prompts/01-requirements/prompt.md
2. Copy the full content
3. Paste into Claude / ChatGPT
4. Replace [SYSTEM_NAME] with "Inventory Management System"
5. Replace [BUSINESS_GOAL] with "Reduce inventory processing time by 50%"
6. Send the message — the AI will generate a Requirements Document
```

### Option B: Single Role (Recommended for specific tasks)

If you only need a specific role (e.g., just Code Review), use only that role's prompt directly.

**Example scenarios**:
- Have existing code, need a review → use `05-code-review/prompt.md`
- Need to design a database → use `02-architecture/prompt.md`
- Need to create a test plan → use `07-qa-testing/prompt.md`

### Option C: Sequential Workflow

1. Start with Role 1 (Requirement Analyst) — produces Requirements Document
2. Feed the output from Role 1 into Role 2 (System Architect) — produces Architecture
3. Feed the output from Role 2 into Role 3 (UX/UI Designer) — produces UI Design
4. Continue through the pipeline until complete

> **Tip**: Each Role's output serves as input for the next Role.
> The more detailed the input, the better the output quality.

---

## Step 4: Customize

- Modify templates to fit your team's specific needs
- Add or remove roles based on project size
- Adjust the Definition of Done criteria to your organization's standards
- Update technology-specific details to match your actual stack

---

## Tips & Best Practices

| Tip | Details |
|-----|---------|
| Start with Requirements | Always use the **Requirement Analyst** prompt first to define project scope |
| Invest in Architecture | The **Architecture** phase is critical — spend adequate time here |
| Never skip Security | Always run a **Security** review before deployment |
| Document continuously | Update **Documentation** alongside development, not just at the end |
| Communicate with Stakeholders | Use **PM templates** for progress reporting |
| Use MoSCoW | Always prioritize with Must / Should / Could / Won't |
| Build MVP first | Select only "Must have" items for the first release |

---

## Usage Modes

| Mode | Best For | How to Use |
|------|----------|------------|
| **Full Simulation** | New projects from scratch | Use all Roles sequentially 1→10 |
| **Single Role** | Specific tasks | Pick only the Role you need |
| **Template Only** | Teams with real people | Use templates as document structures only |
| **Hybrid** | Small teams + AI assistance | Humans do some Roles + AI does others |

---

## Real-World Scenarios

### Scenario 1: Building a New System from Scratch

```
1. Fill in project details in CLAUDE.md
2. Use Role 1 (Requirements) → Get User Stories + Priority Matrix
3. Use Role 2 (Architecture) → Get Architecture + Tech Stack + API Spec
4. Use Role 3 (UX/UI) → Get Design System + Wireframes
5. Start building with Role 4 (Development)
6. Validate with Roles 5-7 (Review + Security + QA)
7. Deploy with Role 8 (DevOps)
8. Create docs with Role 9 (Documentation)
```

### Scenario 2: Adding a Feature to an Existing System

```
1. Use Role 1 (Requirements) → Write User Stories for the new feature only
2. Use Role 2 (Architecture) → Design the parts that need changes
3. Build with Role 4 (Development)
4. Review with Role 5 (Code Review)
5. Test with Role 7 (QA)
```

### Scenario 3: Reviewing Existing Code

```
1. Use Role 5 (Code Review) → Assess code quality
2. Use Role 6 (Security) → Check for vulnerabilities
3. Fix issues based on feedback
```

---

## File Structure

```
.
├── CLAUDE.md                          # Main project configuration
├── .ai-prompts/                       # AI prompts for each Role
│   ├── 01-requirements/prompt.md      #   Requirement Analyst
│   ├── 02-architecture/prompt.md      #   System Architect
│   ├── 03-ux-ui/prompt.md             #   UX/UI Designer
│   ├── 04-development/prompt.md       #   Software Developer
│   ├── 05-code-review/prompt.md       #   Code Reviewer
│   ├── 06-security/prompt.md          #   Security Engineer
│   ├── 07-qa-testing/prompt.md        #   QA / Tester
│   ├── 08-devops/prompt.md            #   DevOps Engineer
│   ├── 09-documentation/prompt.md     #   Technical Writer
│   └── 10-project-management/prompt.md #  Product Owner / PM
│
├── templates/                         # Deliverable templates
│   ├── 01-requirements/               #   Requirements docs (4 files)
│   ├── 02-architecture/               #   Architecture docs (6 files)
│   ├── 03-ux-ui/                      #   UI design docs (5 files)
│   ├── 04-development/                #   Development docs (4 files)
│   ├── 05-code-review/                #   Code review docs (2 files)
│   ├── 06-security/                   #   Security docs (5 files)
│   ├── 07-qa-testing/                 #   QA testing docs (5 files)
│   ├── 08-devops/                     #   DevOps docs (6 files)
│   ├── 09-documentation/              #   User-facing docs (5 files)
│   └── 10-project-management/         #   PM docs (5 files)
│
├── standards/                         # Company-wide baseline standards
│   ├── coding-standards.md            #   Naming, TDD, Git, Security baseline
│   └── tech-stack-catalog.md          #   Approved tech stack catalog
│
├── docs/
│   ├── workflow.md                    # SDLC workflow diagram
│   ├── how-to-use-en.md              # This file (English)
│   ├── how-to-use-th.md              # Thai version
│   └── improvement-recommendations.md # Change log & recommendations
│
└── README.md                          # Project overview
```

---

## FAQ

### Q: Do I have to use all 10 Roles?
**A**: No. Pick only the Roles you need. At minimum, we recommend: Requirements → Architecture → Development → Code Review → QA.

### Q: Which AI tools are compatible?
**A**: Any AI that accepts text input — Claude, ChatGPT, Gemini, Copilot, and more.

### Q: Must I follow the exact order?
**A**: It's recommended because each Role's output feeds into the next. However, for standalone tasks you can skip ahead.

### Q: Can I customize the templates?
**A**: Absolutely. Every template is designed to be modified to fit your team's and project's specific needs.

### Q: What project size is this for?
**A**: Any size — from small projects (use 3-4 Roles) to enterprise-scale (use all 10 Roles).
