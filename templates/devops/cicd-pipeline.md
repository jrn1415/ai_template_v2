# CI/CD Pipeline Configuration

## Project: [SYSTEM_NAME]

---

## Pipeline Overview

```
┌──────────┐    ┌──────────┐    ┌──────────┐    ┌──────────┐    ┌──────────┐
│  Source   │───→│  Build   │───→│   Test   │───→│  Deploy  │───→│  Verify  │
│  (Push)   │    │          │    │          │    │          │    │          │
└──────────┘    └──────────┘    └──────────┘    └──────────┘    └──────────┘
                     │               │               │               │
                  Lint &          Unit +          Staging →       Smoke +
                 Compile       Integration        Prod          Health
                                Security                        Check
```

## Pipeline Stages

### Stage 1: Build

| Step | Command | Timeout | On Failure |
|------|---------|---------|-----------|
| Checkout | `git checkout` | 1 min | Abort |
| Install dependencies | `[npm ci]` | 5 min | Abort |
| Lint | `[npm run lint]` | 3 min | Abort |
| Type check | `[npm run typecheck]` | 3 min | Abort |
| Build | `[npm run build]` | 10 min | Abort |
| Build Docker image | `docker build` | 10 min | Abort |

### Stage 2: Test

| Step | Command | Timeout | On Failure |
|------|---------|---------|-----------|
| Unit tests | `[npm run test]` | 10 min | Abort |
| Integration tests | `[npm run test:integration]` | 15 min | Abort |
| Coverage check | `[coverage >= 80%]` | 1 min | Abort |
| Security scan (SAST) | `[snyk/trivy]` | 10 min | Warn (Critical=Abort) |
| Dependency audit | `[npm audit]` | 5 min | Warn |

### Stage 3: Quality Gate

| Check | Threshold | On Failure |
|-------|-----------|-----------|
| Test coverage | >= 80% | Block |
| No Critical vulnerabilities | 0 | Block |
| Lint errors | 0 | Block |
| Build size | < [X]MB | Warn |

### Stage 4: Deploy

| Environment | Trigger | Strategy | Approval |
|-------------|---------|----------|----------|
| Dev | Push to `develop` | Direct | None |
| Staging | Push to `main` | Blue-Green | None |
| Production | Tag `v*` or manual | Canary | Manual approval |

### Stage 5: Post-Deploy Verification

| Check | Method | Timeout | On Failure |
|-------|--------|---------|-----------|
| Health check | HTTP GET /health | 2 min | Rollback |
| Smoke tests | Automated suite | 5 min | Rollback |
| Monitoring check | Alert rules | 15 min | Alert + Evaluate |

## GitHub Actions Example

```yaml
# .github/workflows/ci-cd.yml
name: CI/CD Pipeline

on:
  push:
    branches: [main, develop]
  pull_request:
    branches: [main]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: '[VERSION]'
          cache: 'npm'
      - run: npm ci
      - run: npm run lint
      - run: npm run build

  test:
    needs: build
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: npm ci
      - run: npm run test -- --coverage
      - run: npm run test:integration

  security:
    needs: build
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: npm audit --audit-level=high
      # Add SAST tool step

  deploy-staging:
    needs: [test, security]
    if: github.ref == 'refs/heads/main'
    runs-on: ubuntu-latest
    environment: staging
    steps:
      - name: Deploy to Staging
        run: echo "Deploy commands here"

  deploy-production:
    needs: deploy-staging
    if: startsWith(github.ref, 'refs/tags/v')
    runs-on: ubuntu-latest
    environment: production
    steps:
      - name: Deploy to Production
        run: echo "Deploy commands here"
```

## Rollback Procedure

1. Detect failure (automated alert or manual)
2. Trigger rollback: `[command/button]`
3. Verify rollback: health check + smoke tests
4. Notify team via [Slack/Teams]
5. Post-mortem: Root cause analysis
