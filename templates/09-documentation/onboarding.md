# Developer Onboarding Guide

## [SYSTEM_NAME]

Welcome to the team! This guide will help you get set up and productive.

---

## Day 1: Environment Setup

### Prerequisites

| Tool | Version | Install Command |
|------|---------|----------------|
| Git | >= 2.x | `brew install git` |
| [Node.js/Python/Go] | >= [X.X] | [install command] |
| Docker | >= [X.X] | [install command] |
| [IDE] | Latest | [download link] |

### Repository Setup

```bash
# 1. Clone the repository
git clone [REPO_URL]
cd [PROJECT_NAME]

# 2. Install dependencies
[npm install / pip install -r requirements.txt]

# 3. Copy environment config
cp .env.example .env
# Edit .env with your local settings

# 4. Start infrastructure (database, cache)
docker compose up -d

# 5. Run database migrations
[migration command]

# 6. Seed development data
[seed command]

# 7. Start development server
[dev server command]

# 8. Verify: open http://localhost:[PORT]
```

### IDE Setup

**Recommended Extensions:**
| Extension | Purpose |
|-----------|---------|
| [ESLint/Pylint] | Code linting |
| [Prettier/Black] | Code formatting |
| [GitLens] | Git integration |
| [Docker] | Docker support |

---

## Day 2: Architecture Overview

### Project Structure
```
[Refer to README for project structure]
```

### Key Concepts
1. **[Concept 1]**: [Brief explanation]
2. **[Concept 2]**: [Brief explanation]
3. **[Concept 3]**: [Brief explanation]

### Architecture Diagram
[Refer to templates/02-architecture/architecture-diagram.md]

---

## Day 3: Development Workflow

### Git Workflow

```
main ─────────────────────────────────
  │                    ↑
  └── feature/xxx ─────┘ (PR + Review)
```

1. Create branch: `git checkout -b feature/[TICKET]-description`
2. Write code + tests
3. Commit: `git commit -m "feat(scope): description"`
4. Push: `git push -u origin feature/[TICKET]-description`
5. Create PR using template
6. Address review feedback
7. Merge after approval

### Commit Convention

```
<type>(<scope>): <description>

Types: feat, fix, docs, style, refactor, test, chore
```

### Running Tests

```bash
# All tests
[npm test]

# With coverage
[npm run test:cov]

# Specific file
[npm test -- path/to/test]
```

---

## Week 1: First Contribution

### Your First PR

1. Pick a "good first issue" from the backlog
2. Follow the development workflow above
3. Submit PR using the template
4. Respond to review feedback

### Code Review Process

- All PRs require at least 1 approval
- Address all comments before merge
- Keep PRs small (< 400 lines)

---

## Key Contacts

| Role | Name | Contact |
|------|------|---------|
| Tech Lead | [Name] | [contact] |
| Product Owner | [Name] | [contact] |
| DevOps | [Name] | [contact] |
| QA Lead | [Name] | [contact] |

## Useful Links

| Resource | URL |
|----------|-----|
| Documentation | [URL] |
| CI/CD Dashboard | [URL] |
| Monitoring | [URL] |
| Design Files | [URL] |
| Project Board | [URL] |
