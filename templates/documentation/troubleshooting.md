# Troubleshooting Guide

## [SYSTEM_NAME]

---

## Common Issues

### Issue 1: Application won't start

**Symptoms**: Server fails to start, error in console

**Possible Causes & Solutions**:

| Cause | Solution |
|-------|---------|
| Port already in use | `lsof -i :[PORT]` then `kill [PID]` |
| Missing .env file | `cp .env.example .env` and fill values |
| Database not running | `docker compose up -d db` |
| Wrong Node/Python version | Use version manager (nvm/pyenv) |
| Missing dependencies | Delete node_modules, run `npm ci` |

### Issue 2: Database connection failed

**Symptoms**: "Connection refused" or timeout errors

**Solutions**:
1. Verify database is running: `docker compose ps`
2. Check DATABASE_URL in .env
3. Verify credentials
4. Check network/firewall

### Issue 3: Tests failing

**Symptoms**: Test suite failures on local or CI

**Solutions**:
1. Pull latest code: `git pull origin main`
2. Reinstall dependencies: `npm ci`
3. Reset test database: `[reset command]`
4. Check test environment variables
5. Run specific failing test for detailed output

### Issue 4: [Common Issue]

**Symptoms**: [Description]

**Solutions**:
1. [Solution step]

---

## Error Code Reference

| Error Code | Message | Cause | Solution |
|-----------|---------|-------|---------|
| E001 | [message] | [cause] | [solution] |
| E002 | [message] | [cause] | [solution] |

---

## Debug Tips

### Logging
```bash
# Set debug log level
LOG_LEVEL=debug [start command]

# Filter logs
[command] | grep "ERROR"
```

### Database Debugging
```sql
-- Check active connections
SELECT * FROM pg_stat_activity WHERE state = 'active';

-- Find slow queries
SELECT query, calls, mean_exec_time FROM pg_stat_statements
ORDER BY mean_exec_time DESC LIMIT 10;
```

### API Debugging
- Use browser DevTools Network tab
- Use Postman/Insomnia for isolated API calls
- Check request/response headers
- Verify authentication token

---

## Escalation

If you cannot resolve the issue:

1. Check this guide and project documentation
2. Search existing issues in the repository
3. Ask in team chat channel
4. Create a new issue with:
   - Steps to reproduce
   - Expected vs actual behavior
   - Environment details
   - Relevant logs
