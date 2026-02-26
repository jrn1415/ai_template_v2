# Pull Request Template

## Use this as `.github/pull_request_template.md` in your repository

---

```markdown
## Description

<!-- Brief description of what this PR does -->

**Related Issue**: #[ISSUE_NUMBER]
**Type**: Feature / Bug Fix / Refactor / Docs / Test / Chore

## Changes Made

<!-- List the specific changes in this PR -->
- [ ] Change 1
- [ ] Change 2
- [ ] Change 3

## Screenshots (if applicable)

<!-- Add screenshots for UI changes -->
| Before | After |
|--------|-------|
| [screenshot] | [screenshot] |

## How to Test

<!-- Step-by-step instructions for reviewers -->
1. Checkout this branch
2. Run `[command]`
3. Navigate to `[location]`
4. Verify `[expected behavior]`

## Checklist

### Code Quality
- [ ] Code follows the project's coding standards
- [ ] Self-reviewed my own code
- [ ] No unnecessary console.log / print statements
- [ ] No hardcoded values (use config/env)
- [ ] Error handling is implemented

### Testing
- [ ] Unit tests added/updated
- [ ] Integration tests added/updated (if applicable)
- [ ] All existing tests pass
- [ ] Test coverage >= 80%

### Documentation
- [ ] Code comments added for complex logic
- [ ] README updated (if applicable)
- [ ] API docs updated (if applicable)

### Security
- [ ] No sensitive data in code (keys, passwords, tokens)
- [ ] Input validation implemented
- [ ] SQL injection / XSS prevention verified
- [ ] Authorization checks in place

### Database
- [ ] Migration script included (if schema changed)
- [ ] Rollback script included
- [ ] No breaking changes to existing data

## Dependencies

<!-- List any dependent PRs or external dependencies -->
- Depends on PR #[NUMBER]
- Requires [external service/config change]

## Deployment Notes

<!-- Any special deployment instructions -->
- [ ] Environment variable changes needed
- [ ] Database migration required
- [ ] Cache invalidation needed
- [ ] Feature flag configuration needed
```
