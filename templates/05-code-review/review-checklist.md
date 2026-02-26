# Code Review Checklist

## Project: [SYSTEM_NAME]

Use this checklist for every Pull Request review.

---

## 1. Correctness

- [ ] Code implements the requirement correctly
- [ ] Edge cases are handled
- [ ] Error handling is appropriate
- [ ] No off-by-one errors
- [ ] Null/undefined checks where needed
- [ ] Race conditions considered (if applicable)

## 2. Code Quality

- [ ] Follows SOLID principles
- [ ] No code duplication (DRY)
- [ ] Functions/methods are small and focused
- [ ] Naming is clear and descriptive
- [ ] No magic numbers/strings (use constants)
- [ ] Appropriate abstraction level
- [ ] No dead code / commented-out code

## 3. Security

- [ ] No hardcoded secrets or credentials
- [ ] Input validation on all user inputs
- [ ] SQL injection prevention (parameterized queries)
- [ ] XSS prevention (output encoding)
- [ ] Authentication checks on protected endpoints
- [ ] Authorization checks (role/permission based)
- [ ] Sensitive data not logged

## 4. Performance

- [ ] No N+1 query problems
- [ ] Appropriate use of indexes
- [ ] No unnecessary database calls
- [ ] Pagination for list endpoints
- [ ] Caching used where appropriate
- [ ] No memory leaks (event listeners, subscriptions)
- [ ] Algorithm complexity is acceptable

## 5. Testing

- [ ] Unit tests cover new/changed code
- [ ] Edge cases tested
- [ ] Error scenarios tested
- [ ] Test names are descriptive
- [ ] Tests are independent (no shared state)
- [ ] Coverage meets minimum (>= 80%)
- [ ] No flaky tests introduced

## 6. Documentation

- [ ] Complex logic has comments
- [ ] Public APIs are documented
- [ ] README updated if needed
- [ ] CHANGELOG updated if needed
- [ ] ADR created for significant decisions

## 7. Architecture

- [ ] Follows established patterns in the codebase
- [ ] No unnecessary dependencies added
- [ ] Proper separation of concerns
- [ ] Database schema changes are backward compatible
- [ ] API changes are backward compatible (or versioned)

## 8. Git

- [ ] Commit messages follow convention
- [ ] No unnecessary files committed
- [ ] PR is appropriately sized (< 400 lines ideally)
- [ ] Branch is up-to-date with base branch
