# Test Cases

## Project: [SYSTEM_NAME]
## Module: [MODULE_NAME]

---

## Test Case Template

### TC-[MODULE]-001: [Test Case Title]

| Field | Detail |
|-------|--------|
| **Priority** | P0 / P1 / P2 / P3 |
| **Type** | Functional / Integration / E2E |
| **Automation** | Manual / Automated |
| **Related Story** | US-[XXX] |

**Preconditions:**
- [Condition 1]
- [Condition 2]

**Test Steps:**

| Step | Action | Expected Result | Actual Result | Status |
|------|--------|-----------------|---------------|--------|
| 1 | [action] | [expected] | [actual] | Pass/Fail |
| 2 | [action] | [expected] | [actual] | Pass/Fail |
| 3 | [action] | [expected] | [actual] | Pass/Fail |

**Test Data:**
| Data | Value |
|------|-------|
| [field] | [value] |

**Postconditions:**
- [Expected system state after test]

---

### TC-[MODULE]-002: [Test Case Title]

[Same structure]

---

## Test Case Summary

| TC ID | Title | Priority | Type | Status | Last Run |
|-------|-------|----------|------|--------|----------|
| TC-AUTH-001 | Login with valid credentials | P0 | Functional | Pass | [date] |
| TC-AUTH-002 | Login with invalid password | P0 | Functional | Pass | [date] |
| TC-AUTH-003 | Login with locked account | P1 | Functional | Fail | [date] |
| | | | | | |

## Coverage Matrix

| User Story | Test Cases | Covered | Status |
|-----------|-----------|---------|--------|
| US-001 | TC-001, TC-002, TC-003 | 3/3 | Complete |
| US-002 | TC-004, TC-005 | 2/2 | Complete |
| US-003 | TC-006 | 1/3 | In Progress |
