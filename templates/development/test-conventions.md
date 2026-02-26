# Testing Conventions

## Project: [SYSTEM_NAME]

---

## Testing Strategy

| Type | Coverage Target | Tools | Runner |
|------|----------------|-------|--------|
| Unit Tests | >= 80% | [Jest/Pytest/Go test] | CI |
| Integration Tests | Critical paths | [Supertest/Pytest/httptest] | CI |
| E2E Tests | Critical user flows | [Playwright/Cypress] | CI |
| Performance Tests | Key endpoints | [k6/Artillery/JMeter] | Manual/Scheduled |

## Naming Convention

### Test Files
```
src/services/user.service.ts        → tests/unit/services/user.service.test.ts
src/controllers/auth.controller.ts  → tests/unit/controllers/auth.controller.test.ts
src/repositories/order.repo.ts      → tests/integration/repositories/order.repo.test.ts
```

### Test Names
Use the pattern: `should [expected behavior] when [condition]`

```
describe('UserService', () => {
  describe('createUser', () => {
    it('should create user when valid data provided')
    it('should throw ValidationError when email is invalid')
    it('should throw ConflictError when email already exists')
  })
})
```

## Test Structure (AAA Pattern)

```
// Arrange - Setup test data and conditions
const userData = { email: 'test@example.com', name: 'Test' }
const mockRepo = { create: jest.fn().mockResolvedValue(userData) }

// Act - Execute the function under test
const result = await userService.createUser(userData)

// Assert - Verify the expected outcome
expect(result.email).toBe('test@example.com')
expect(mockRepo.create).toHaveBeenCalledWith(userData)
```

## What to Test

### Unit Tests
- [ ] Business logic in services
- [ ] Validation functions
- [ ] Utility functions
- [ ] Data transformations
- [ ] Error handling paths
- [ ] Edge cases (null, empty, boundary values)

### Integration Tests
- [ ] API endpoint request/response
- [ ] Database CRUD operations
- [ ] Authentication flows
- [ ] Authorization (role-based access)
- [ ] Third-party service integrations (with mocks)

### Do NOT Test
- Framework internals
- Third-party library code
- Simple getters/setters
- Constants

## Mocking Guidelines

| Dependency | Mock Strategy |
|-----------|---------------|
| Database | In-memory DB or Repository mock |
| External APIs | HTTP interceptor (nock/responses) |
| File System | Virtual filesystem or mock |
| Time/Date | Freeze time (jest.useFakeTimers) |
| Random values | Seed or mock |

## Test Data

- Use factories/fixtures for consistent test data
- Never use production data in tests
- Clean up test data after each test
- Use unique identifiers to prevent test interference

## Coverage Requirements

| Metric | Minimum | Target |
|--------|---------|--------|
| Line Coverage | 80% | 90% |
| Branch Coverage | 70% | 85% |
| Function Coverage | 80% | 90% |

**Excluded from coverage:**
- Configuration files
- Type definitions
- Index/barrel files
- Migration files
