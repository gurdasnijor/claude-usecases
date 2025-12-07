# CI/CD Pipeline Designer

> Design and implement automated build, test, and deployment pipelines

## Overview

The CI/CD Pipeline Designer creates robust continuous integration and deployment workflows. It supports GitHub Actions, GitLab CI, Jenkins, and other platforms with best practices for speed, reliability, and security.

## When to Use

- **Set up new CI/CD** for a project
- **Migrate between platforms** (e.g., Jenkins to GitHub Actions)
- **Optimize slow builds** with caching and parallelization
- **Add deployment stages** for staging/production
- **Implement security scanning** in pipelines

## Supported Platforms

| Platform | Best For |
|----------|----------|
| **GitHub Actions** | GitHub repositories |
| **GitLab CI/CD** | GitLab repositories |
| **Jenkins** | Self-hosted, enterprise |
| **CircleCI** | Fast builds, Docker-native |
| **Azure DevOps** | Microsoft ecosystem |

## Quick Example

**Request:**
```
Create a GitHub Actions workflow for a Node.js project with:
- Linting and type checking
- Unit tests with coverage
- Build step
- Deploy to Vercel on main
```

**Generated Workflow:**
```yaml
name: CI/CD

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  quality:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: '20'
          cache: 'npm'
      - run: npm ci
      - run: npm run lint
      - run: npm run typecheck

  test:
    runs-on: ubuntu-latest
    needs: quality
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: '20'
          cache: 'npm'
      - run: npm ci
      - run: npm test -- --coverage

  deploy:
    runs-on: ubuntu-latest
    needs: test
    if: github.ref == 'refs/heads/main'
    steps:
      - uses: actions/checkout@v4
      - uses: amondnet/vercel-action@v25
        with:
          vercel-token: ${{ secrets.VERCEL_TOKEN }}
          vercel-org-id: ${{ secrets.VERCEL_ORG_ID }}
          vercel-project-id: ${{ secrets.VERCEL_PROJECT_ID }}
          vercel-args: '--prod'
```

## Pipeline Stages

| Stage | Purpose | Examples |
|-------|---------|----------|
| **Lint** | Code quality | ESLint, Prettier, Flake8 |
| **Test** | Correctness | Jest, pytest, go test |
| **Build** | Create artifacts | webpack, Docker, cargo |
| **Security** | Vulnerability scan | npm audit, CodeQL |
| **Deploy** | Release | AWS, Vercel, K8s |

## Key Features

- **Caching** - Speed up builds with dependency caching
- **Matrix builds** - Test across multiple versions
- **Parallelization** - Run independent jobs concurrently
- **Environments** - Separate staging/production configs
- **Secrets** - Secure credential management

## Optimization Tips

| Issue | Solution |
|-------|----------|
| Slow builds | Enable caching, parallel jobs |
| Flaky tests | Add retries, isolate tests |
| High costs | Path filters, skip CI option |
| Long queues | Self-hosted runners |

## Related Skills

- **security-audit-assistant** - Add security scanning
- **test-case-generator** - Generate CI-compatible tests
- **code-review-assistant** - Automated quality checks

## Version

- **Current:** v1.0.0
- **Last Updated:** 2025-12-07
- **Author:** 360 Social Impact Studios
