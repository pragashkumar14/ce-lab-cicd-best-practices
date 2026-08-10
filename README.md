# CI/CD Best Practices — Terraform Infrastructure

![CI Pipeline](https://github.com/pragashkumar14/ce-lab-cicd-best-practices/actions/workflows/ci.yml/badge.svg)
![CD Pipeline](https://github.com/pragashkumar14/ce-lab-cicd-best-practices/actions/workflows/cd.yml/badge.svg)
![Commit Lint](https://github.com/pragashkumar14/ce-lab-cicd-best-practices/actions/workflows/commit-lint.yml/badge.svg)
![Release](https://github.com/pragashkumar14/ce-lab-cicd-best-practices/actions/workflows/release.yml/badge.svg)

## Architecture

This repository manages shared infrastructure resources:
- **S3 Bucket** — Versioned artifact storage with encryption and lifecycle policies
- **DynamoDB Table** — Application state store with point-in-time recovery

## CI/CD Workflows

| Workflow | Trigger | Purpose |
|----------|---------|---------|
| CI Pipeline | PR to `main` | Format, validate, security scan, plan |
| CD Pipeline | Push to `main` | Plan + deploy with manual approval |
| Commit Lint | PR open/edit | Enforce conventional commit titles |
| Release Please | Push to `main` | Automated versioning and changelog |

## Environment Protection

The `production` environment requires:
- **Required reviewer approval** before `terraform apply` runs
- **5-minute wait timer** after approval, before deployment proceeds

## Prerequisites

- Terraform `>= 1.15.8`
- AWS credentials configured as repository secrets:
  - `AWS_ACCESS_KEY_ID`
  - `AWS_SECRET_ACCESS_KEY`

## Quick Start

```bash
cd terraform
terraform init
terraform plan
terraform apply
```
