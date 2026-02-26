# Tech Stack Catalog — [COMPANY_NAME]

> **ระดับ:** Company-wide Approved Stack
> **ใช้กับ:** ทุกโปรเจกต์ที่ใช้ AI Template นี้
> **เจ้าของ:** System Architect / CTO
> **อัปเดตล่าสุด:** [DATE]
> **Version:** 1.0

> **วิธีใช้:**
> - Architect เลือก stack จาก catalog นี้สำหรับแต่ละโปรเจกต์
> - ถ้าต้องการใช้ "Not Approved" ต้องผ่าน Architecture Decision Record (ADR) ก่อน
> - บันทึกการเลือกสุดท้ายใน `templates/02-architecture/tech-stack.md` ของโปรเจกต์

---

## Status Legend

| Status | ความหมาย |
|--------|---------|
| ✅ Approved | ใช้ได้เลย — บริษัทรองรับและมี expertise |
| ⚠️ Conditional | ใช้ได้ในบาง use case — ดูเงื่อนไขที่ระบุ |
| 🔬 Evaluation | กำลังทดสอบ — ใช้ใน non-critical project เท่านั้น |
| ❌ Not Approved | ห้ามใช้ — ต้องทำ ADR ก่อน |

---

## 1. Frontend

### Web Framework
| Technology | Status | Use Case | หมายเหตุ |
|-----------|--------|----------|---------|
| **Next.js 14+** (App Router) | ✅ Approved | Web app (SSR/SSG/SPA) | Default choice |
| **React 18+** (Vite) | ✅ Approved | SPA ที่ไม่ต้องการ SSR | เมื่อ Next.js เกินความจำเป็น |
| **Vue 3** | ⚠️ Conditional | Web app | ใช้ถ้า team มี expertise — ต้องระบุเหตุผล |
| Angular | ❌ Not Approved | — | ไม่มี expertise ใน team |

### Mobile
| Technology | Status | Use Case | หมายเหตุ |
|-----------|--------|----------|---------|
| **React Native + Expo** | ✅ Approved | Cross-platform mobile | Default choice |
| **Flutter** | ⚠️ Conditional | Cross-platform mobile | ถ้า team มี Dart expertise |
| Native iOS / Android | ⚠️ Conditional | Performance-critical app | ต้องมี justification ชัดเจน |

### UI Component Library
| Technology | Status | หมายเหตุ |
|-----------|--------|---------|
| **Tailwind CSS** | ✅ Approved | Default styling approach |
| **shadcn/ui** | ✅ Approved | Component library สำหรับ Next.js/React |
| **Ant Design** | ⚠️ Conditional | Admin dashboards — bundle size ใหญ่ |
| Material UI | ⚠️ Conditional | ถ้า client ต้องการ Material design explicitly |

### State Management
| Technology | Status | Use Case |
|-----------|--------|---------|
| **Zustand** | ✅ Approved | Client state (เบา, simple) |
| **TanStack Query** | ✅ Approved | Server state / data fetching |
| Redux Toolkit | ⚠️ Conditional | Complex global state — ต้องมีเหตุผล |

---

## 2. Backend

> **Primary:** .NET 10 (LTS) — บริษัทใช้ C#/.NET เป็น backend หลัก

### API Framework
| Technology | Status | Use Case | หมายเหตุ |
|-----------|--------|----------|---------|
| **ASP.NET Core 10 (Minimal API)** | ✅ Approved | REST API — lightweight, high-perf | **Default backend** — ใช้สำหรับ new projects |
| **ASP.NET Core 10 (MVC/Controllers)** | ✅ Approved | REST API — large codebase, structured | ใช้เมื่อ team ต้องการ convention over configuration |
| **Node.js + Fastify** | ⚠️ Conditional | JS/TS microservice รอง | ถ้า service นั้น team JS-only หรือ frontend-driven |
| **FastAPI** | ⚠️ Conditional | Python microservice (ML/AI pipeline) | เฉพาะ service ที่ต้องใช้ Python ecosystem |
| **Go + Gin** | ⚠️ Conditional | Ultra-high-throughput service | ถ้า team มี Go expertise + justified perf requirement |

### API Design
- **Standard**: RESTful API (default)
- **Versioning**: URL path versioning — `/api/v1/`, `/api/v2/`
- **Format**: JSON (application/json) — ใช้ `System.Text.Json` (built-in .NET) ไม่ใช้ Newtonsoft ยกเว้นมีเหตุผล
- GraphQL: ⚠️ Conditional — ใช้ Hot Chocolate หรือ Strawberry Shake ถ้าต้องการ GraphQL ใน .NET

---

## 3. Database

### Relational (SQL)
| Technology | Status | Use Case | หมายเหตุ |
|-----------|--------|----------|---------|
| **PostgreSQL 15+** | ✅ Approved | Primary database | Default choice |
| **MySQL 8+** | ⚠️ Conditional | Legacy system integration | ใช้ PostgreSQL แทนถ้าเป็นไปได้ |
| SQLite | ⚠️ Conditional | Development / testing / edge | ไม่ใช้ใน production (web app) |

### NoSQL
| Technology | Status | Use Case | หมายเหตุ |
|-----------|--------|----------|---------|
| **Redis 7+** | ✅ Approved | Cache / Session / Queue | Default caching layer |
| **MongoDB** | ⚠️ Conditional | Document store | ต้องมี use case ชัดเจน (เช่น unstructured content) |
| Elasticsearch | ⚠️ Conditional | Full-text search / analytics | ถ้าต้องการ search ที่ซับซ้อน |

### ORM / Query Builder
| Technology | Status | ใช้กับ | หมายเหตุ |
|-----------|--------|-------|---------|
| **Entity Framework Core 10** | ✅ Approved | .NET / C# | **Default ORM** — Code First + Migrations |
| **Dapper** | ✅ Approved | .NET / C# | ใช้เมื่อต้องการ performance สูง / complex SQL |
| **Prisma** | ✅ Approved | Node.js/TypeScript | สำหรับ JS/TS services |
| **SQLAlchemy 2.0** | ✅ Approved | Python | สำหรับ Python services |
| **TypeORM** | ⚠️ Conditional | Node.js | ใช้ Prisma แทนถ้าเป็นไปได้ |

> **EF Core vs Dapper guideline:** ใช้ EF Core เป็น default — ถ้า query ซับซ้อน หรือ performance test พิสูจน์ว่า EF Core ช้าเกินไป ให้ใช้ Dapper สำหรับ query นั้นๆ (ผสมกันได้ใน project เดียวกัน)

---

## 4. Infrastructure & DevOps

### Cloud Provider
| Technology | Status | หมายเหตุ |
|-----------|--------|---------|
| **AWS** | ✅ Approved | Default cloud provider |
| **GCP** | ⚠️ Conditional | ถ้า client อยู่บน GCP แล้ว |
| **Azure** | ⚠️ Conditional | ถ้า client อยู่บน Azure แล้ว |

### Container & Orchestration
| Technology | Status | Use Case |
|-----------|--------|---------|
| **Docker** | ✅ Approved | All deployments |
| **Docker Compose** | ✅ Approved | Local development |
| **Kubernetes (EKS/GKE)** | ⚠️ Conditional | ≥ 5 services หรือ high traffic |

### CI/CD
| Technology | Status | หมายเหตุ |
|-----------|--------|---------|
| **GitHub Actions** | ✅ Approved | Default CI/CD |
| **GitLab CI** | ⚠️ Conditional | ถ้า client ใช้ GitLab |

### Infrastructure as Code
| Technology | Status | หมายเหตุ |
|-----------|--------|---------|
| **Terraform** | ✅ Approved | Default IaC |
| **Bicep (Azure)** | ✅ Approved | ถ้า deploy บน Azure — native ARM template ที่อ่านง่ายกว่า |
| **AWS CDK** | ⚠️ Conditional | ถ้า team ถนัด TypeScript IaC |

---

## 5. Authentication & Security

| Technology | Status | Use Case | หมายเหตุ |
|-----------|--------|----------|---------|
| **ASP.NET Core Identity** | ✅ Approved | User management ใน .NET app | Built-in, เชื่อมกับ EF Core ได้ทันที |
| **JWT Bearer (.NET)** | ✅ Approved | Stateless auth ใน .NET API | `Microsoft.AspNetCore.Authentication.JwtBearer` — access token ≤ 24h |
| **Duende IdentityServer** | ⚠️ Conditional | OAuth2/OIDC provider (self-hosted) | ถ้าต้องการ centralized auth server — มี license cost สำหรับ commercial |
| **NextAuth.js / Auth.js** | ✅ Approved | Next.js frontend auth | รองรับ OAuth providers — ใช้คู่กับ .NET backend |
| **Passport.js** | ⚠️ Conditional | Express auth (JS service) | เฉพาะ Node.js services |
| **Auth0** | ⚠️ Conditional | Managed auth service | ถ้า client ต้องการ managed auth — มี licensing cost |
| **Keycloak** | ⚠️ Conditional | Enterprise SSO (self-hosted) | ทางเลือกแทน Duende ถ้าไม่ต้องการ .NET native |

---

## 6. Messaging & Async

| Technology | Status | Use Case | หมายเหตุ |
|-----------|--------|----------|---------|
| **MassTransit + RabbitMQ** | ✅ Approved | Message bus (.NET) | **Default สำหรับ .NET** — abstracts transport, รองรับ Saga/Outbox pattern |
| **Hangfire** | ✅ Approved | Background jobs / scheduled tasks (.NET) | ใช้ PostgreSQL หรือ Redis เป็น storage |
| **Azure Service Bus** | ⚠️ Conditional | Managed message broker | ถ้า deploy บน Azure และต้องการ enterprise features |
| **AWS SQS + SNS** | ⚠️ Conditional | Managed queue (AWS) | ถ้า all-in AWS |
| **Apache Kafka** | ⚠️ Conditional | Event streaming | ถ้า throughput > 100k msg/s — ใช้ Confluent .NET client |
| **BullMQ** (Redis-based) | ⚠️ Conditional | Job queue (Node.js services) | เฉพาะ Node.js services |
| **Celery** | ⚠️ Conditional | Task queue (Python services) | เฉพาะ Python services |

---

## 7. Monitoring & Observability

| Technology | Status | Use Case |
|-----------|--------|---------|
| **Sentry** | ✅ Approved | Error tracking (frontend + backend) |
| **Grafana + Prometheus** | ✅ Approved | Metrics + dashboards |
| **Loki** | ✅ Approved | Log aggregation |
| **AWS CloudWatch** | ⚠️ Conditional | ถ้า all-in AWS infra |
| Datadog | ⚠️ Conditional | ถ้า client มี Datadog subscription |

---

## 8. AI / LLM Integration

| Technology | Status | Use Case | หมายเหตุ |
|-----------|--------|----------|---------|
| **Claude API (Anthropic)** | ✅ Approved | LLM features | Default LLM — claude-sonnet-4-6 |
| **OpenAI API** | ⚠️ Conditional | ถ้า client กำหนด | ระบุ model version ชัดเจน |
| **LangChain** | 🔬 Evaluation | LLM orchestration | ยังประเมินอยู่ |
| **Vercel AI SDK** | ✅ Approved | AI streaming ใน Next.js | |

---

## 9. การเลือก Stack สำหรับโปรเจกต์ใหม่

### Decision Flow

```
โปรเจกต์ใหม่
    ↓
มี special requirement? (e.g., client mandate, existing system)
    ├── ใช่ → ดู Conditional options + สร้าง ADR ถ้าต้อง
    └── ไม่ → ใช้ Default Stack ด้านล่าง
```

### Default Stack (Recommended for New Projects)

```
Frontend:   Next.js 14+ + Tailwind CSS + shadcn/ui + Zustand + TanStack Query
Backend:    ASP.NET Core 10 (Minimal API) + C# 13
ORM:        Entity Framework Core 10 (+ Dapper สำหรับ performance-critical queries)
Database:   PostgreSQL 15+ + Redis 7+
Auth:       ASP.NET Core Identity + JWT Bearer
Messaging:  MassTransit + RabbitMQ (ถ้าต้องการ async) | Hangfire (ถ้าต้องการ background jobs)
DevOps:     Docker + GitHub Actions + AWS (ECS) หรือ Azure (AKS/App Service)
Monitoring: Sentry + Grafana + Prometheus
```

### เมื่อ Backend เป็น Python (ML/AI service เท่านั้น)

```
Backend:    FastAPI + Python 3.12+
Database:   PostgreSQL 15+ + Redis 7+ + SQLAlchemy 2.0
Queue:      Celery + Redis
```

> **หมายเหตุ:** Python service ควรเป็น standalone microservice ที่ .NET backend เรียกผ่าน HTTP/gRPC
> ไม่ควร mix Python logic ลงใน .NET project โดยตรง

---

## 10. Architecture Decision Record (ADR) — เมื่อต้องออกนอก Catalog

ถ้าต้องการใช้ technology ที่ไม่อยู่ใน Approved list ให้สร้าง ADR ใน:
`templates/02-architecture/adr-log.md`

**ADR ต้องมี:**
1. Context: ทำไมถึงต้องการ tech นี้
2. Alternatives Considered: ลอง Approved options แล้วยังไง
3. Decision: เลือกอะไร
4. Consequences: trade-offs ที่ยอมรับ
5. Approved by: [ชื่อ Architect/CTO]
