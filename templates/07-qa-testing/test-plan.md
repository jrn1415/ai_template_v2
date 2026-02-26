# Test Plan

## Project: [SYSTEM_NAME]
**Version**: [VERSION]
**Date**: [DATE]
**QA Lead**: [NAME]

---

## 1. Test Scope

### In Scope
| # | Module/Feature | Type of Testing |
|---|---------------|----------------|
| 1 | [feature] | Functional, Performance |
| 2 | [feature] | Functional, Security |

### Out of Scope
| # | Module/Feature | Reason |
|---|---------------|--------|
| 1 | [feature] | [reason] |

## 2. Test Strategy

| Test Type | Approach | Tools | Automation |
|-----------|----------|-------|-----------|
| Unit Testing | Developer-owned | [Jest/Pytest] | Automated |
| Integration Testing | API-level | [Supertest/Postman] | Automated |
| Functional Testing | Feature-level | Manual + [Playwright] | Partial |
| Regression Testing | Suite-based | [Playwright/Cypress] | Automated |
| Performance Testing | Load/Stress | [k6/Artillery] | Automated |
| Security Testing | OWASP-based | [OWASP ZAP] | Semi-auto |
| UAT | User acceptance | Manual | Manual |

## 3. Test Environment

| Environment | URL | Database | Purpose |
|-------------|-----|----------|---------|
| QA | qa.[domain].com | QA DB (seeded) | Functional testing |
| Staging | staging.[domain].com | Staging DB (prod-like) | Pre-production |
| Performance | perf.[domain].com | Perf DB (scaled data) | Performance testing |

## 4. Entry Criteria

- [ ] Code deployed to QA environment
- [ ] All unit tests passing
- [ ] Code review approved
- [ ] Test data prepared
- [ ] Test environment verified

## 5. Exit Criteria

- [ ] All P0/P1 test cases passed
- [ ] No Critical/High bugs open
- [ ] Test coverage >= [X]%
- [ ] Performance targets met
- [ ] Security scan passed
- [ ] QA sign-off obtained

## 6. Test Schedule

| Phase | Start | End | Responsible |
|-------|-------|-----|-------------|
| Test Planning | [date] | [date] | QA Lead |
| Test Case Design | [date] | [date] | QA Team |
| Test Execution | [date] | [date] | QA Team |
| Bug Fix & Retest | [date] | [date] | Dev + QA |
| Regression | [date] | [date] | QA Team |
| Sign-off | [date] | [date] | QA Lead |

## 7. Risk Assessment

| Risk | Impact | Probability | Mitigation |
|------|--------|------------|------------|
| Environment instability | High | Medium | Dedicated QA env |
| Incomplete requirements | High | Medium | Early review sessions |
| Resource shortage | Medium | Low | Cross-training |

## 8. Defect Management

| Severity | Description | SLA (Fix) | SLA (Retest) |
|----------|-------------|-----------|-------------|
| Critical | System crash, data loss | 4 hours | 1 hour |
| High | Major feature broken | 1 day | 4 hours |
| Medium | Feature works with workaround | 3 days | 1 day |
| Low | Cosmetic, minor issues | Next sprint | Next sprint |
