# CI/CD Pipeline — TechShop Online Store
**Version:** 1.0 | **Date:** 2026-03-16 | **Author:** DevOps Engineer AI

---

## Pipeline Overview

```
Code Push → PR → CI Pipeline → Merge → CD Pipeline → Deploy
```

### CI Pipeline (Pull Request)

```
┌─────────────────────────────────────────────────┐
│ CI Pipeline — runs on every PR                   │
│                                                   │
│  [1] Checkout + Setup                             │
│       ↓                                           │
│  [2] Build (.NET + npm)                           │
│       ↓ fail → block merge                        │
│  [3] Unit Tests + Coverage                        │
│       ↓ coverage < 80% → fail                     │
│  [4] Security Scan (dotnet-security-scan + npm audit)│
│       ↓ Critical vuln → fail                      │
│  [5] Integration Tests                            │
│       ↓ fail → block merge                        │
│  [6] Quality Gate (all green?)                    │
│       ↓ Yes → Allow merge                         │
└─────────────────────────────────────────────────┘
```

### CD Pipeline (Main Branch)

```
┌─────────────────────────────────────────────────┐
│ CD Pipeline — runs on merge to main               │
│                                                   │
│  [1] Build + Test (re-run CI)                     │
│       ↓                                           │
│  [2] Build Docker Images                          │
│       ↓                                           │
│  [3] Push to Container Registry (ACR)             │
│       ↓                                           │
│  [4] Deploy to Staging                            │
│       ↓                                           │
│  [5] Smoke Tests on Staging                       │
│       ↓ fail → rollback + alert                   │
│  [6] Manual Approval Gate (Production)            │
│       ↓ Approved                                  │
│  [7] Deploy to Production (Canary 10% → 100%)     │
│       ↓                                           │
│  [8] Smoke Tests + Monitor (30 min)               │
│       ↓ error rate spike → auto rollback          │
└─────────────────────────────────────────────────┘
```

---

## GitHub Actions: CI Workflow

```yaml
# .github/workflows/ci.yml
name: CI — Build, Test, Security

on:
  pull_request:
    branches: [main, develop]

jobs:
  build-test:
    runs-on: ubuntu-latest
    services:
      postgres:
        image: postgres:16
        env:
          POSTGRES_DB: techshop_test
          POSTGRES_PASSWORD: test_password
        ports: ["5432:5432"]
      redis:
        image: redis:7
        ports: ["6379:6379"]

    steps:
      - uses: actions/checkout@v4

      - name: Setup .NET 10
        uses: actions/setup-dotnet@v4
        with:
          dotnet-version: '10.0.x'

      - name: Restore & Build
        run: dotnet build --no-incremental -c Release

      - name: Run Tests with Coverage
        run: |
          dotnet test --collect:"XPlat Code Coverage" \
            --results-directory ./coverage \
            -- DataCollectionRunSettings.DataCollectors.DataCollector.Configuration.Format=cobertura
        env:
          ConnectionStrings__DefaultConnection: "Host=localhost;Database=techshop_test;Username=postgres;Password=test_password"
          Redis__ConnectionString: "localhost:6379"

      - name: Coverage Gate (80%)
        run: |
          COVERAGE=$(grep -oP 'line-rate="\K[^"]+' coverage/*/coverage.cobertura.xml | head -1)
          echo "Coverage: $COVERAGE"
          awk "BEGIN{exit ($COVERAGE < 0.8)}" || (echo "Coverage below 80%!" && exit 1)

      - name: Security Scan
        run: |
          dotnet list package --vulnerable --include-transitive
          npm audit --audit-level=high

      - name: Frontend Build
        run: |
          cd frontend
          npm ci
          npm run build
```

---

## Docker Configuration

```dockerfile
# Backend: src/TechShop.API/Dockerfile
FROM mcr.microsoft.com/dotnet/sdk:10.0 AS build
WORKDIR /src
COPY ["TechShop.API/TechShop.API.csproj", "TechShop.API/"]
RUN dotnet restore "TechShop.API/TechShop.API.csproj"
COPY . .
RUN dotnet publish "TechShop.API/TechShop.API.csproj" -c Release -o /app/publish

FROM mcr.microsoft.com/dotnet/aspnet:10.0 AS runtime
WORKDIR /app
# Run as non-root user
RUN addgroup --system appgroup && adduser --system --ingroup appgroup appuser
USER appuser
COPY --from=build /app/publish .
EXPOSE 8080
ENTRYPOINT ["dotnet", "TechShop.API.dll"]
```

---

## Environment Configuration

| Variable | Staging | Production | Notes |
|----------|---------|------------|-------|
| `ConnectionStrings__DefaultConnection` | Azure Staging DB | Azure Prod DB | PostgreSQL 16 Flexible |
| `Redis__ConnectionString` | Redis Staging | Redis Prod | Azure Cache for Redis |
| `Jwt__Secret` | Key Vault (Staging) | Key Vault (Prod) | Never in code |
| `Stripe__SecretKey` | Test key (sk_test_...) | Live key (sk_live_...) | Never in code |
| `Stripe__WebhookSecret` | Test webhook secret | Prod webhook secret | Webhook validation |
| `SendGrid__ApiKey` | Test mode | Production | Email delivery |
| `ASPNETCORE_ENVIRONMENT` | Staging | Production | Affects logging level |

---

## Deployment Strategy

### Canary Deployment (Production)

1. Deploy new version → 10% traffic
2. Monitor 15 minutes: error rate, P95 latency, CPU
3. If healthy → 50% → monitor 15 min
4. If healthy → 100%
5. If error rate > 5% at any stage → auto rollback

### Rollback Procedure

```bash
# Emergency rollback (< 2 minutes)
az container app revision deactivate --name techshop-api \
  --revision-name techshop-api--[new-revision]

# Or: repoint traffic to previous revision
az container app ingress traffic set --name techshop-api \
  --revision-weight [previous-revision]=100
```

---

## Monitoring & Alerting

| Metric | Tool | Alert Threshold |
|--------|------|-----------------|
| Error Rate | Application Insights | > 5% in 5 min → PagerDuty |
| P95 Latency | Application Insights | > 1000ms → Slack alert |
| CPU Usage | Azure Monitor | > 80% for 5 min → scale out |
| DB Connections | PostgreSQL metrics | > 80% pool → alert |
| Failed Payments | Stripe Dashboard | > 10% failure rate → PagerDuty |
| SSL Expiry | Cloudflare | < 30 days → alert |

---

## Handoff Digest → Role 9: Technical Writer

**Status:** READY

**Critical Items for Next Role:**
- CI/CD: GitHub Actions (ดู .github/workflows/)
- Environments: Staging + Production บน Azure (Container Apps + PostgreSQL Flexible)
- API Base URLs: Staging: https://api-staging.techshop.th/v1 | Prod: https://api.techshop.th/v1
- Frontend: Hosted บน Vercel (https://techshop.th)

**Key Deliverables Created:**
- `templates/08-devops/cicd-pipeline.md` ✅
- `templates/08-devops/infrastructure.md` ✅
- `templates/08-devops/docker-config.md` ✅
- `templates/08-devops/monitoring.md` ✅
- `templates/08-devops/runbooks.md` ✅
- `templates/08-devops/environments.md` ✅
