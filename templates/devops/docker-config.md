# Docker Configuration

## Project: [SYSTEM_NAME]

---

## Dockerfile (Multi-stage Build)

```dockerfile
# ============================================
# Stage 1: Dependencies
# ============================================
FROM node:[VERSION]-alpine AS deps
WORKDIR /app
COPY package*.json ./
RUN npm ci --only=production

# ============================================
# Stage 2: Build
# ============================================
FROM node:[VERSION]-alpine AS build
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
RUN npm run build

# ============================================
# Stage 3: Production
# ============================================
FROM node:[VERSION]-alpine AS production

# Security: non-root user
RUN addgroup -g 1001 -S appgroup && \
    adduser -S appuser -u 1001 -G appgroup

WORKDIR /app

COPY --from=deps /app/node_modules ./node_modules
COPY --from=build /app/dist ./dist
COPY package*.json ./

# Security: read-only filesystem where possible
USER appuser

EXPOSE [PORT]

HEALTHCHECK --interval=30s --timeout=3s --retries=3 \
  CMD wget --no-verbose --tries=1 --spider http://localhost:[PORT]/health || exit 1

CMD ["node", "dist/main.js"]
```

## Docker Compose (Development)

```yaml
# docker-compose.yml
version: '3.8'

services:
  app:
    build:
      context: .
      dockerfile: Dockerfile
      target: build
    ports:
      - "[PORT]:[PORT]"
    environment:
      - NODE_ENV=development
      - DATABASE_URL=postgresql://user:pass@db:5432/[DB_NAME]
      - REDIS_URL=redis://cache:6379
    volumes:
      - .:/app
      - /app/node_modules
    depends_on:
      db:
        condition: service_healthy
      cache:
        condition: service_healthy
    command: npm run dev

  db:
    image: postgres:[VERSION]-alpine
    ports:
      - "5432:5432"
    environment:
      POSTGRES_USER: user
      POSTGRES_PASSWORD: pass
      POSTGRES_DB: [DB_NAME]
    volumes:
      - pgdata:/var/lib/postgresql/data
    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U user"]
      interval: 5s
      timeout: 5s
      retries: 5

  cache:
    image: redis:[VERSION]-alpine
    ports:
      - "6379:6379"
    healthcheck:
      test: ["CMD", "redis-cli", "ping"]
      interval: 5s
      timeout: 5s
      retries: 5

volumes:
  pgdata:
```

## .dockerignore

```
node_modules
npm-debug.log
.git
.gitignore
.env
.env.*
docker-compose*.yml
Dockerfile
README.md
docs/
tests/
coverage/
.vscode/
.idea/
```

## Image Optimization Checklist

- [ ] Multi-stage build (separate deps/build/runtime)
- [ ] Alpine-based images (smaller size)
- [ ] Non-root user
- [ ] .dockerignore configured
- [ ] Health check defined
- [ ] No secrets in image layers
- [ ] Pinned base image versions
- [ ] Layer caching optimized (COPY order)
