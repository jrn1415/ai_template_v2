# API Specification

## Project: [SYSTEM_NAME]
**Base URL**: `https://api.[domain].com/v1`
**API Version**: v1
**Authentication**: Bearer Token (JWT)

---

## General Conventions

### Request Format
- Content-Type: `application/json`
- Accept: `application/json`
- Authorization: `Bearer <token>`

### Response Format

```json
{
  "success": true,
  "data": { ... },
  "meta": {
    "page": 1,
    "per_page": 20,
    "total": 100,
    "total_pages": 5
  }
}
```

### Error Response

```json
{
  "success": false,
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Human-readable error message",
    "details": [
      {
        "field": "email",
        "message": "Invalid email format"
      }
    ]
  }
}
```

### HTTP Status Codes

| Code | Meaning | Usage |
|------|---------|-------|
| 200 | OK | Successful GET, PUT, PATCH |
| 201 | Created | Successful POST |
| 204 | No Content | Successful DELETE |
| 400 | Bad Request | Validation error |
| 401 | Unauthorized | Missing/invalid token |
| 403 | Forbidden | Insufficient permissions |
| 404 | Not Found | Resource not found |
| 409 | Conflict | Duplicate resource |
| 422 | Unprocessable | Business logic error |
| 429 | Too Many Requests | Rate limited |
| 500 | Internal Error | Server error |

---

## Endpoints

### Authentication

#### POST /auth/register
Register a new user.

**Request:**
```json
{
  "email": "user@example.com",
  "password": "SecurePass123!",
  "name": "John Doe"
}
```

**Response (201):**
```json
{
  "success": true,
  "data": {
    "id": "uuid",
    "email": "user@example.com",
    "name": "John Doe",
    "created_at": "2025-01-01T00:00:00Z"
  }
}
```

#### POST /auth/login
Authenticate user and get tokens.

**Request:**
```json
{
  "email": "user@example.com",
  "password": "SecurePass123!"
}
```

**Response (200):**
```json
{
  "success": true,
  "data": {
    "access_token": "eyJhbG...",
    "refresh_token": "eyJhbG...",
    "token_type": "Bearer",
    "expires_in": 3600
  }
}
```

#### POST /auth/refresh
Refresh access token.

#### POST /auth/logout
Invalidate current session.

---

### Resource: [RESOURCE_NAME]

#### GET /[resources]
List all resources (paginated).

**Query Parameters:**
| Param | Type | Default | Description |
|-------|------|---------|-------------|
| page | int | 1 | Page number |
| per_page | int | 20 | Items per page (max 100) |
| sort | string | created_at | Sort field |
| order | string | desc | Sort order (asc/desc) |
| search | string | - | Search keyword |
| filter[field] | string | - | Filter by field |

**Response (200):**
```json
{
  "success": true,
  "data": [ ... ],
  "meta": {
    "page": 1,
    "per_page": 20,
    "total": 100,
    "total_pages": 5
  }
}
```

#### GET /[resources]/:id
Get single resource by ID.

#### POST /[resources]
Create new resource.

#### PUT /[resources]/:id
Update resource (full replacement).

#### PATCH /[resources]/:id
Partial update resource.

#### DELETE /[resources]/:id
Delete resource.

---

## Rate Limiting

| Endpoint | Rate Limit | Window |
|----------|-----------|--------|
| POST /auth/* | 10 requests | 1 minute |
| GET /* | 100 requests | 1 minute |
| POST/PUT/PATCH /* | 30 requests | 1 minute |
| DELETE /* | 10 requests | 1 minute |

**Rate Limit Headers:**
```
X-RateLimit-Limit: 100
X-RateLimit-Remaining: 95
X-RateLimit-Reset: 1640000000
```

## Versioning Strategy

- URL-based versioning: `/v1/`, `/v2/`
- Breaking changes require new version
- Old versions supported for minimum 6 months after deprecation notice
