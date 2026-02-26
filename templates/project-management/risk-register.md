# Risk Register

## [SYSTEM_NAME]
**Last Updated**: [DATE]

---

## Risk Matrix

```
              Impact
              Low    Medium   High    Critical
Probability ┌────────┬────────┬────────┬────────┐
High        │ Medium │  High  │Critical│Critical│
            ├────────┼────────┼────────┼────────┤
Medium      │  Low   │ Medium │  High  │Critical│
            ├────────┼────────┼────────┼────────┤
Low         │  Low   │  Low   │ Medium │  High  │
            └────────┴────────┴────────┴────────┘
```

## Active Risks

| ID | Category | Risk | Probability | Impact | Score | Mitigation | Owner | Status |
|----|----------|------|-------------|--------|-------|-----------|-------|--------|
| R-001 | Technical | [Risk description] | High | High | Critical | [Plan] | [Name] | Open |
| R-002 | Resource | [Risk description] | Medium | Medium | Medium | [Plan] | [Name] | Monitoring |
| R-003 | Business | [Risk description] | Low | High | Medium | [Plan] | [Name] | Open |
| R-004 | External | [Risk description] | Medium | Low | Low | [Plan] | [Name] | Open |
| R-005 | Schedule | [Risk description] | | | | | | |

## Risk Categories

| Category | Description | Examples |
|----------|-------------|---------|
| Technical | Technology-related risks | Performance, scalability, integration |
| Resource | People and skills | Key person dependency, hiring |
| Business | Market and business changes | Requirements change, budget cuts |
| External | Third-party dependencies | Vendor reliability, API changes |
| Schedule | Timeline risks | Delays, underestimation |
| Security | Security threats | Data breach, vulnerabilities |

## Mitigated Risks

| ID | Risk | Original Score | Mitigation Applied | Current Score | Date |
|----|------|---------------|-------------------|---------------|------|
| R-010 | [Risk] | High | [What was done] | Low | [Date] |

## Closed Risks

| ID | Risk | Reason for Closure | Date |
|----|------|-------------------|------|
| R-020 | [Risk] | [Did not materialize / Resolved] | [Date] |

## Risk Review Schedule

| Review Type | Frequency | Participants | Next Review |
|-------------|----------|-------------|-------------|
| Quick scan | Weekly | PM + Tech Lead | [Date] |
| Full review | Bi-weekly | Full team | [Date] |
| Stakeholder review | Monthly | PM + Stakeholders | [Date] |
