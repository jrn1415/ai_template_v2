# Architecture Diagram

## Project: [SYSTEM_NAME]

---

## High-Level Architecture

```mermaid
graph TB
    subgraph "Client Layer"
        WEB[Web App<br/>React/Vue/Angular]
        MOBILE[Mobile App<br/>React Native/Flutter]
    end

    subgraph "API Gateway"
        GW[API Gateway<br/>Kong/AWS API GW]
        LB[Load Balancer<br/>Nginx/ALB]
    end

    subgraph "Application Layer"
        API[API Server<br/>Node.js/Python/Go]
        AUTH[Auth Service<br/>JWT/OAuth]
        WS[WebSocket Server<br/>Real-time]
    end

    subgraph "Data Layer"
        DB[(Primary DB<br/>PostgreSQL/MySQL)]
        CACHE[(Cache<br/>Redis)]
        SEARCH[(Search<br/>Elasticsearch)]
        QUEUE[Message Queue<br/>RabbitMQ/Kafka]
    end

    subgraph "Storage"
        S3[Object Storage<br/>S3/GCS]
        CDN[CDN<br/>CloudFront]
    end

    subgraph "Monitoring"
        MON[Monitoring<br/>Prometheus]
        LOG[Logging<br/>ELK Stack]
        ALERT[Alerting<br/>PagerDuty]
    end

    WEB --> GW
    MOBILE --> GW
    GW --> LB
    LB --> API
    LB --> AUTH
    LB --> WS
    API --> DB
    API --> CACHE
    API --> SEARCH
    API --> QUEUE
    API --> S3
    S3 --> CDN
    API --> MON
    API --> LOG
    MON --> ALERT
```

## Component Diagram

```mermaid
graph LR
    subgraph "Frontend"
        UI[UI Components]
        STATE[State Management]
        ROUTER[Router]
        HTTP[HTTP Client]
    end

    subgraph "Backend"
        CTRL[Controllers]
        SVC[Services]
        REPO[Repositories]
        MW[Middleware]
    end

    subgraph "Shared"
        DTO[DTOs/Models]
        VALID[Validators]
        UTIL[Utilities]
    end

    UI --> STATE
    STATE --> HTTP
    HTTP --> MW
    MW --> CTRL
    CTRL --> SVC
    SVC --> REPO
    CTRL --> DTO
    SVC --> VALID
```

## Infrastructure Diagram

```
┌─────────────────────────────────────────────────────┐
│                    Cloud Provider                     │
│  ┌─────────────────────────────────────────────────┐ │
│  │                    VPC                           │ │
│  │  ┌──────────┐  ┌──────────┐  ┌──────────────┐  │ │
│  │  │ Public   │  │ Private  │  │ Database     │  │ │
│  │  │ Subnet   │  │ Subnet   │  │ Subnet       │  │ │
│  │  │          │  │          │  │              │  │ │
│  │  │ [LB]     │  │ [App]    │  │ [DB Primary] │  │ │
│  │  │ [NAT GW] │  │ [App]    │  │ [DB Replica] │  │ │
│  │  │ [Bastion]│  │ [Worker] │  │ [Redis]      │  │ │
│  │  └──────────┘  └──────────┘  └──────────────┘  │ │
│  └─────────────────────────────────────────────────┘ │
│                                                       │
│  [S3] [CloudFront] [Route53] [ACM]                   │
└─────────────────────────────────────────────────────┘
```

## Decision Records

| Decision | Options Considered | Chosen | Reason |
|----------|-------------------|--------|--------|
| Architecture Style | Monolith, Microservices, Modular Monolith | [chosen] | [reason] |
| Communication | REST, GraphQL, gRPC | [chosen] | [reason] |
| Database | SQL vs NoSQL | [chosen] | [reason] |
