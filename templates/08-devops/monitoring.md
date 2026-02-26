# Monitoring & Observability

## Project: [SYSTEM_NAME]

---

## Monitoring Stack

| Component | Tool | Purpose |
|-----------|------|---------|
| Metrics | [Prometheus/CloudWatch/Datadog] | Time-series metrics |
| Logging | [ELK/Loki/CloudWatch] | Log aggregation |
| Tracing | [Jaeger/X-Ray/Datadog APM] | Distributed tracing |
| Dashboard | [Grafana/CloudWatch/Datadog] | Visualization |
| Alerting | [PagerDuty/OpsGenie/Slack] | Incident notification |

## Key Metrics (RED Method)

### Request Metrics

| Metric | Description | Alert Threshold |
|--------|-------------|----------------|
| Request Rate | Requests per second | Anomaly detection |
| Error Rate | % of 5xx responses | > 1% |
| Duration (p50) | Median response time | > [X]ms |
| Duration (p95) | 95th percentile | > [X]ms |
| Duration (p99) | 99th percentile | > [X]ms |

### Resource Metrics (USE Method)

| Resource | Utilization | Saturation | Errors |
|----------|-------------|------------|--------|
| CPU | % usage | Load average | - |
| Memory | % used | Swap usage | OOM kills |
| Disk | % capacity | I/O wait | I/O errors |
| Network | Bandwidth | Connection queue | Packet loss |

### Business Metrics

| Metric | Description | Dashboard |
|--------|-------------|-----------|
| Active Users | Concurrent users | Main |
| Sign-ups | New registrations/day | Main |
| Transaction Volume | Transactions/hour | Main |
| Error Rate by Feature | Errors per feature | Detail |

## Alert Rules

| Alert | Condition | Severity | Notification | Runbook |
|-------|-----------|----------|-------------|---------|
| High Error Rate | error_rate > 5% for 5m | Critical | PagerDuty + Slack | [link] |
| Slow Response | p95 > [X]ms for 10m | Warning | Slack | [link] |
| High CPU | cpu > 85% for 10m | Warning | Slack | [link] |
| Disk Space | disk > 80% | Warning | Slack | [link] |
| Service Down | health_check fail for 1m | Critical | PagerDuty | [link] |
| High Memory | memory > 90% for 5m | Critical | PagerDuty + Slack | [link] |
| DB Connection Pool | pool > 80% for 5m | Warning | Slack | [link] |

## Dashboard Layout

### Main Dashboard
- Request rate (graph)
- Error rate (graph)
- Response time p50/p95/p99 (graph)
- Active users (single stat)
- Service health status (status map)
- Resource utilization (gauge panels)

### Detail Dashboard
- Per-endpoint metrics
- Database query performance
- Cache hit/miss ratio
- Queue depth & processing time
- Dependency health

## Logging Standards

### Log Levels

| Level | Usage | Example |
|-------|-------|---------|
| ERROR | Errors requiring attention | Failed DB query, unhandled exception |
| WARN | Abnormal but handled | Rate limited, retry succeeded |
| INFO | Normal operations | Request handled, user action |
| DEBUG | Development details | Variable values, flow trace |

### Log Format

```json
{
  "timestamp": "2025-01-01T00:00:00.000Z",
  "level": "INFO",
  "service": "[SERVICE_NAME]",
  "trace_id": "abc-123",
  "message": "Request processed",
  "context": {
    "method": "GET",
    "path": "/api/users",
    "status": 200,
    "duration_ms": 45,
    "user_id": "usr_xxx"
  }
}
```

### Log Retention

| Environment | Retention | Storage |
|-------------|----------|---------|
| Production | 90 days | [S3/CloudWatch] |
| Staging | 30 days | [S3/CloudWatch] |
| Development | 7 days | Local |
