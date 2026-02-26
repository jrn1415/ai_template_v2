# Runbooks

## Project: [SYSTEM_NAME]

---

## RB-001: Service Health Check Failure

### Symptoms
- Health check endpoint returns non-200
- Monitoring alerts triggered
- Users report service unavailability

### Diagnosis Steps

1. **Check service status**
   ```bash
   # Kubernetes
   kubectl get pods -n [NAMESPACE]
   kubectl describe pod [POD_NAME] -n [NAMESPACE]

   # Docker
   docker ps -a | grep [SERVICE]
   docker logs [CONTAINER_ID] --tail 100
   ```

2. **Check application logs**
   ```bash
   kubectl logs [POD_NAME] -n [NAMESPACE] --tail 200
   ```

3. **Check resource utilization**
   ```bash
   kubectl top pods -n [NAMESPACE]
   kubectl top nodes
   ```

4. **Check dependencies**
   - Database connectivity
   - Cache connectivity
   - External service health

### Resolution

| Issue | Resolution | Command |
|-------|-----------|---------|
| Pod crash loop | Check logs, fix config | `kubectl logs [POD] --previous` |
| OOM killed | Increase memory limit | Update deployment manifest |
| Dependency down | Check dependency service | See dependency runbook |
| Config error | Fix config, redeploy | `kubectl rollout restart` |

### Rollback

```bash
# Kubernetes rollback
kubectl rollout undo deployment/[DEPLOYMENT] -n [NAMESPACE]

# Verify rollback
kubectl rollout status deployment/[DEPLOYMENT] -n [NAMESPACE]
```

---

## RB-002: High Error Rate

### Symptoms
- Error rate > 5% for 5+ minutes
- Alert: "High Error Rate"

### Diagnosis Steps

1. Check error logs for patterns
2. Identify affected endpoints
3. Check recent deployments
4. Check dependency health
5. Check for traffic anomalies

### Resolution
- If deployment-related: Rollback
- If dependency-related: See dependency runbook
- If traffic-related: Scale up, enable rate limiting

---

## RB-003: Database Connection Issues

### Symptoms
- "Connection refused" or timeout errors
- Slow queries
- Connection pool exhaustion

### Diagnosis Steps

1. **Check DB status**
   ```bash
   # Check connection count
   SELECT count(*) FROM pg_stat_activity;

   # Check long-running queries
   SELECT pid, now() - pg_stat_activity.query_start AS duration, query
   FROM pg_stat_activity
   WHERE state != 'idle'
   ORDER BY duration DESC;
   ```

2. **Check DB resources**: CPU, Memory, Disk, IOPS

3. **Check application connection pool**

### Resolution

| Issue | Resolution |
|-------|-----------|
| Too many connections | Increase pool size or fix connection leaks |
| Slow queries | Add indexes, optimize queries |
| Disk full | Clean up, expand storage |
| Replication lag | Check network, reduce write load |

---

## RB-004: Deployment Rollback Procedure

1. Identify the issue and confirm rollback is needed
2. Execute rollback command
3. Verify health checks pass
4. Monitor for 15 minutes
5. Notify team and stakeholders
6. Create incident report

---

## Escalation Path

| Level | Contact | Response Time | Criteria |
|-------|---------|--------------|----------|
| L1 | On-call engineer | 15 min | Alert triggered |
| L2 | Team lead | 30 min | L1 cannot resolve |
| L3 | Engineering manager | 1 hour | Service-wide impact |
| L4 | VP Engineering | 2 hours | Business-critical outage |
