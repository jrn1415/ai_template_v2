# Infrastructure as Code

## Project: [SYSTEM_NAME]
**Cloud Provider**: [AWS/GCP/Azure]
**IaC Tool**: [Terraform/CloudFormation/Pulumi]

---

## Architecture Overview

```
┌─────────────────────────────────────────────────┐
│                   [Cloud Provider]                │
│                                                   │
│  ┌─── Region: [REGION] ──────────────────────┐   │
│  │                                            │   │
│  │  ┌─── VPC: 10.0.0.0/16 ─────────────────┐│   │
│  │  │                                        ││   │
│  │  │  Public Subnet     Private Subnet      ││   │
│  │  │  10.0.1.0/24       10.0.2.0/24        ││   │
│  │  │  ┌──────────┐     ┌──────────┐        ││   │
│  │  │  │ ALB      │     │ App (x2) │        ││   │
│  │  │  │ NAT GW   │     │ Worker   │        ││   │
│  │  │  └──────────┘     └──────────┘        ││   │
│  │  │                                        ││   │
│  │  │  DB Subnet                             ││   │
│  │  │  10.0.3.0/24                           ││   │
│  │  │  ┌──────────┐     ┌──────────┐        ││   │
│  │  │  │ Primary  │     │ Replica  │        ││   │
│  │  │  │ DB       │     │ DB       │        ││   │
│  │  │  └──────────┘     └──────────┘        ││   │
│  │  │                                        ││   │
│  │  └────────────────────────────────────────┘│   │
│  └────────────────────────────────────────────┘   │
│                                                   │
│  [S3]  [CloudFront]  [Route53]  [ACM]            │
└─────────────────────────────────────────────────┘
```

## Resource Inventory

| Resource | Service | Count | Est. Monthly Cost |
|----------|---------|-------|-------------------|
| Compute | [EC2/ECS/EKS] | [X] | $[X] |
| Database | [RDS/Aurora] | [X] | $[X] |
| Cache | [ElastiCache] | [X] | $[X] |
| Storage | [S3] | [X] GB | $[X] |
| CDN | [CloudFront] | - | $[X] |
| DNS | [Route53] | [X] zones | $[X] |
| Load Balancer | [ALB] | [X] | $[X] |
| Monitoring | [CloudWatch] | - | $[X] |
| **Total** | | | **$[X]/month** |

## Terraform Module Structure

```
infrastructure/
├── environments/
│   ├── dev/
│   │   ├── main.tf
│   │   ├── variables.tf
│   │   └── terraform.tfvars
│   ├── staging/
│   │   └── ...
│   └── production/
│       └── ...
├── modules/
│   ├── networking/
│   │   ├── main.tf
│   │   ├── variables.tf
│   │   └── outputs.tf
│   ├── compute/
│   ├── database/
│   ├── cache/
│   └── monitoring/
└── README.md
```

## Disaster Recovery

| Metric | Target | Strategy |
|--------|--------|----------|
| RPO (Recovery Point Objective) | [X] minutes | Automated backups |
| RTO (Recovery Time Objective) | [X] minutes | Multi-AZ + auto-failover |
| Backup Frequency | Every [X] hours | Automated |
| Backup Retention | [X] days | Lifecycle policy |
| DR Region | [REGION] | Cross-region replication |
