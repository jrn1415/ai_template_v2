# API Documentation

## [SYSTEM_NAME] API
**Version**: v1
**Base URL**: `https://api.[domain].com/v1`

---

## Authentication

All API requests require a Bearer token in the Authorization header.

```
Authorization: Bearer <your_access_token>
```

### Getting a Token

```bash
curl -X POST https://api.[domain].com/v1/auth/login \
  -H "Content-Type: application/json" \
  -d '{"email": "user@example.com", "password": "your_password"}'
```

**Response:**
```json
{
  "access_token": "eyJhbG...",
  "token_type": "Bearer",
  "expires_in": 3600
}
```

---

## Endpoints

### [Resource Name]

#### List [Resources]

```
GET /[resources]
```

**Parameters:**
| Name | In | Type | Required | Description |
|------|-----|------|----------|-------------|
| page | query | integer | No | Page number (default: 1) |
| per_page | query | integer | No | Items per page (default: 20) |

**Example:**
```bash
curl https://api.[domain].com/v1/[resources]?page=1&per_page=20 \
  -H "Authorization: Bearer <token>"
```

**Response (200):**
```json
{
  "success": true,
  "data": [],
  "meta": { "page": 1, "total": 0 }
}
```

#### Get [Resource]

```
GET /[resources]/:id
```

#### Create [Resource]

```
POST /[resources]
```

**Body:**
```json
{
  "field1": "value1",
  "field2": "value2"
}
```

#### Update [Resource]

```
PUT /[resources]/:id
```

#### Delete [Resource]

```
DELETE /[resources]/:id
```

---

## Error Codes

| Code | Message | Description |
|------|---------|-------------|
| VALIDATION_ERROR | Validation failed | Check request body |
| NOT_FOUND | Resource not found | Invalid ID |
| UNAUTHORIZED | Authentication required | Missing/invalid token |
| FORBIDDEN | Access denied | Insufficient permissions |
| RATE_LIMITED | Too many requests | Wait and retry |

---

## SDKs & Libraries

| Language | Package | Installation |
|----------|---------|-------------|
| JavaScript | [@org/sdk] | `npm install @org/sdk` |
| Python | [org-sdk] | `pip install org-sdk` |

---

## Changelog

| Version | Date | Changes |
|---------|------|---------|
| v1.0 | [DATE] | Initial release |
