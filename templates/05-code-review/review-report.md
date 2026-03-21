# Code Review Report

## PR: [PR_TITLE] (#[PR_NUMBER])

| Field | Detail |
|-------|--------|
| **Reviewer** | [REVIEWER_NAME] |
| **Author** | [AUTHOR_NAME] |
| **Date** | [DATE] |
| **Branch** | [feature/xxx] → [main] |
| **Files Changed** | [X] files |
| **Lines** | +[X] / -[X] |

---

## Summary

[2-3 ประโยคสรุปภาพรวมของการ review]

## Verdict

- [ ] **APPROVED** - Ready to merge
- [ ] **REQUEST CHANGES** - Must fix before merge
- [ ] **COMMENT** - Feedback only, non-blocking

---

## Findings

### Critical Issues (Must Fix)

| # | File:Line | Issue | Suggestion |
|---|-----------|-------|-----------|
| 1 | `src/file.ts:42` | [Description] | [How to fix] |
| 2 | | | |

### Warnings (Should Fix)

| # | File:Line | Issue | Suggestion |
|---|-----------|-------|-----------|
| 1 | `src/file.ts:85` | [Description] | [How to fix] |
| 2 | | | |

### Suggestions (Nice to Have)

| # | File:Line | Suggestion | Benefit |
|---|-----------|-----------|---------|
| 1 | `src/file.ts:120` | [Suggestion] | [Why it's better] |
| 2 | | | |

### Positive Feedback

- [Something done well]
- [Good pattern used]

---

## Review Checklist

### 1. Correctness
- [ ] Code implements the requirement correctly (Acceptance Criteria met)
- [ ] Edge cases are handled
- [ ] Error handling is appropriate
- [ ] Null/undefined checks where needed
- [ ] Race conditions considered (if applicable)

### 2. Code Quality
- [ ] Follows SOLID principles — no violations found
- [ ] No code duplication (DRY)
- [ ] Functions/methods are small and focused (≤ 20 lines)
- [ ] Naming is clear and descriptive (self-documenting)
- [ ] No magic numbers/strings (constants/enums used)
- [ ] No dead code or commented-out code

### 3. Security
- [ ] No hardcoded secrets or credentials
- [ ] Input validation on all user inputs (at controller/route level)
- [ ] Parameterized queries — no string concatenation in SQL
- [ ] Authentication checks on protected endpoints
- [ ] Authorization checks (role/permission based)
- [ ] Sensitive data not logged

### 4. Performance
- [ ] No N+1 query problems
- [ ] Pagination for list endpoints
- [ ] No unnecessary DB calls in loops
- [ ] Caching used where appropriate
- [ ] Algorithm complexity is acceptable

### 5. Testing
- [ ] Tests cover new/changed code (Happy path + Edge cases + Error cases)
- [ ] Test names are descriptive (`MethodName_Scenario_ExpectedResult`)
- [ ] Tests are independent (no shared mutable state)
- [ ] Coverage meets minimum (≥ 80%)
- [ ] No flaky tests introduced

### 6. Architecture & Git
- [ ] Follows established patterns in codebase
- [ ] No unnecessary dependencies added
- [ ] Proper separation of concerns
- [ ] Commit messages follow Conventional Commits format
- [ ] PR is appropriately sized (< 400 lines ideally)
- [ ] API changes are backward compatible (or versioned)

## Review Time

| Metric | Value |
|--------|-------|
| Review Started | [datetime] |
| Review Completed | [datetime] |
| Total Review Time | [X] minutes |
| Iterations | [X] round(s) |
