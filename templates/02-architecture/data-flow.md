# Data Flow & Sequence Diagrams

## Project: [SYSTEM_NAME]

---

## 1. Authentication Flow

```mermaid
sequenceDiagram
    actor User
    participant Client
    participant API as API Gateway
    participant Auth as Auth Service
    participant DB as Database
    participant Cache as Redis

    User->>Client: Enter credentials
    Client->>API: POST /auth/login
    API->>Auth: Validate credentials
    Auth->>DB: Query user by email
    DB-->>Auth: User record
    Auth->>Auth: Verify password hash
    Auth->>Auth: Generate JWT tokens
    Auth->>Cache: Store refresh token
    Auth-->>API: Access + Refresh tokens
    API-->>Client: 200 OK + tokens
    Client->>Client: Store tokens
    Client-->>User: Redirect to dashboard
```

## 2. CRUD Operation Flow

```mermaid
sequenceDiagram
    actor User
    participant Client
    participant API as API Server
    participant MW as Middleware
    participant SVC as Service
    participant DB as Database
    participant Cache as Redis

    User->>Client: Create resource
    Client->>API: POST /resources (+ Bearer token)
    API->>MW: Auth middleware
    MW->>MW: Validate JWT
    MW->>API: User context
    API->>SVC: Create resource
    SVC->>SVC: Validate input
    SVC->>DB: INSERT resource
    DB-->>SVC: Created resource
    SVC->>Cache: Invalidate list cache
    SVC-->>API: Resource DTO
    API-->>Client: 201 Created
    Client-->>User: Show success
```

## 3. Data Processing Flow

```mermaid
graph LR
    A[Input] --> B[Validation]
    B -->|Valid| C[Business Logic]
    B -->|Invalid| D[Error Response]
    C --> E{Async?}
    E -->|Yes| F[Message Queue]
    E -->|No| G[Database]
    F --> H[Worker]
    H --> G
    G --> I[Cache Update]
    I --> J[Response]
```

## 4. Error Handling Flow

```mermaid
sequenceDiagram
    participant Client
    participant API
    participant Service
    participant Logger

    Client->>API: Request
    API->>Service: Process
    Service->>Service: Error occurs!
    Service->>Logger: Log error details
    Service-->>API: Throw AppError
    API->>API: Error handler middleware
    API->>Logger: Log request context
    API-->>Client: Error response (appropriate HTTP code)

    Note over Client,Logger: Error includes: code, message, request_id
    Note over Client,Logger: NO sensitive data in client response
```

## 5. [Custom Flow: FLOW_NAME]

```mermaid
sequenceDiagram
    Note over System: Describe your custom flow here
```

---

## Data Transformation Points

| Point | Input Format | Output Format | Transformation |
|-------|-------------|---------------|----------------|
| API Input | JSON (client) | DTO | Validation + Sanitization |
| Service Layer | DTO | Entity | Business logic |
| Repository | Entity | SQL | ORM mapping |
| API Output | Entity | Response DTO | Field selection + formatting |
