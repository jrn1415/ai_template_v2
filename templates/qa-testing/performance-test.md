# Performance Test Plan

## Project: [SYSTEM_NAME]

---

## Objectives

| Objective | Target Metric |
|-----------|--------------|
| Response time under normal load | p95 < [X]ms |
| Throughput | >= [X] req/sec |
| Error rate under load | < 1% |
| Max concurrent users | [X] users |
| System stability | 24h endurance test pass |

## Test Scenarios

### Scenario 1: Load Test (Normal Traffic)

| Parameter | Value |
|-----------|-------|
| Virtual Users | [X] (ramp up over [X] min) |
| Duration | [X] minutes |
| Think Time | [X] seconds |
| Target RPS | [X] |

**Endpoints:**
| Endpoint | Method | Weight | Expected Response |
|----------|--------|--------|------------------|
| /api/[resource] | GET | 40% | < [X]ms |
| /api/[resource] | POST | 20% | < [X]ms |
| /api/[resource]/:id | GET | 30% | < [X]ms |
| /api/auth/login | POST | 10% | < [X]ms |

### Scenario 2: Stress Test (Peak Traffic)

| Parameter | Value |
|-----------|-------|
| Virtual Users | [X] (2x normal) |
| Duration | [X] minutes |
| Goal | Find breaking point |

### Scenario 3: Spike Test

| Parameter | Value |
|-----------|-------|
| Base Users | [X] |
| Spike Users | [X] (sudden increase) |
| Spike Duration | [X] minutes |
| Goal | Recovery time measurement |

### Scenario 4: Endurance Test

| Parameter | Value |
|-----------|-------|
| Virtual Users | [X] (normal load) |
| Duration | [X] hours |
| Goal | Memory leaks, resource degradation |

## Success Criteria

| Metric | Load Test | Stress Test | Spike Test | Endurance |
|--------|-----------|-------------|-----------|-----------|
| Avg Response Time | < [X]ms | < [X]ms | < [X]ms | < [X]ms |
| p95 Response Time | < [X]ms | < [X]ms | < [X]ms | < [X]ms |
| p99 Response Time | < [X]ms | - | - | < [X]ms |
| Error Rate | < 0.1% | < 5% | < 1% | < 0.1% |
| CPU Usage | < 70% | < 90% | < 90% | < 70% |
| Memory Usage | < 70% | < 90% | < 90% | Stable |
| Recovery Time | N/A | N/A | < [X]s | N/A |

## Results Template

| Metric | Target | Actual | Status |
|--------|--------|--------|--------|
| Avg Response Time | < [X]ms | [X]ms | Pass/Fail |
| p95 Response Time | < [X]ms | [X]ms | Pass/Fail |
| Throughput | [X] rps | [X] rps | Pass/Fail |
| Error Rate | < [X]% | [X]% | Pass/Fail |
| Max VUs Sustained | [X] | [X] | Pass/Fail |

## Bottlenecks Found

| # | Component | Issue | Impact | Recommendation |
|---|-----------|-------|--------|---------------|
| 1 | [component] | [issue] | [impact] | [fix] |
