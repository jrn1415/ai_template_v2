# Environment Configuration

## Project: [SYSTEM_NAME]

---

## Environment Overview

| Environment | Purpose | URL | Deploy Trigger |
|-------------|---------|-----|---------------|
| Development | Local dev | localhost:[PORT] | Manual |
| QA | Testing | qa.[domain].com | Push to `develop` |
| Staging | Pre-prod | staging.[domain].com | Push to `main` |
| Production | Live | [domain].com | Tag `v*` + approval |

## Environment Specs

### Production

| Resource | Specification | Scaling |
|----------|--------------|---------|
| App Servers | [instance type] x [count] | Auto-scale: 2-10 |
| Database | [instance type], [storage] | Read replicas: [count] |
| Cache | [instance type] | Cluster mode |
| CDN | [provider] | Global |
| Load Balancer | [type] | Multi-AZ |

### Staging (Production-like)

| Resource | Specification | Notes |
|----------|--------------|-------|
| App Servers | [smaller instance] x 2 | Same config as prod |
| Database | [smaller instance] | Same schema, subset data |
| Cache | [smaller instance] | Same config |

### QA

| Resource | Specification | Notes |
|----------|--------------|-------|
| App Servers | [minimal instance] x 1 | Reset-able |
| Database | [minimal instance] | Seed data |
| Cache | [minimal instance] | |

## Environment Variables

| Variable | Dev | QA | Staging | Prod | Sensitive |
|----------|-----|-----|---------|------|-----------|
| NODE_ENV | development | qa | staging | production | No |
| DATABASE_URL | local | [url] | [url] | [url] | Yes |
| REDIS_URL | local | [url] | [url] | [url] | Yes |
| JWT_SECRET | dev-secret | [managed] | [managed] | [managed] | Yes |
| LOG_LEVEL | debug | debug | info | warn | No |
| API_URL | localhost | qa.api | staging.api | api | No |

## Promotion Process

```
Dev → QA → Staging → Production
 │     │      │          │
 │     │      │     Manual approval
 │     │      │     + QA sign-off
 │     │      │
 │     │    Automated tests
 │     │    + Security scan
 │     │
 │   QA testing
 │   + Bug fixes
 │
 Development
 + Unit tests
```

## Access Control

| Environment | Developer | QA | DevOps | Manager |
|-------------|-----------|-----|--------|---------|
| Development | Full | Read | Full | Read |
| QA | Read | Full | Full | Read |
| Staging | Read | Read | Full | Read |
| Production | None | None | Full | Read |
