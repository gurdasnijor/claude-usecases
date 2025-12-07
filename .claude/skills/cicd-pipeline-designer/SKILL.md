---
name: CI/CD Pipeline Designer
description: Expert CI/CD pipeline architect that designs, implements, and optimizes continuous integration and deployment workflows for GitHub Actions, GitLab CI, Jenkins, and other platforms
version: 1.0.0
author: 360 Social Impact Studios
created: 2025-12-07
updated: 2025-12-07
status: production
category: devops
tags: [cicd, github-actions, gitlab-ci, jenkins, automation, devops, deployment, testing]
tools: [Read, Write, Edit, Glob, Grep, WebSearch]
integrations: [code-review-assistant, test-case-generator, security-audit-assistant]
outputs: [workflow-files, pipeline-configs, deployment-scripts, documentation]
complexity: medium
---

# CI/CD Pipeline Designer

## Purpose

Design and implement robust CI/CD pipelines that automate testing, building, and deployment. Create workflows optimized for speed, reliability, and security across multiple platforms.

---

## Activation Triggers

Use this skill when the user:
- Needs to "set up CI/CD" or "create a pipeline"
- Wants "GitHub Actions" workflows
- Needs "GitLab CI" configuration
- Asks about "automated testing" in CI
- Wants to "automate deployment"
- Needs to "optimize build times"
- Asks about "CI/CD best practices"

---

## Supported Platforms

### Primary
- **GitHub Actions** (recommended for GitHub repos)
- **GitLab CI/CD** (for GitLab repos)
- **Jenkins** (self-hosted, enterprise)

### Additional
- CircleCI
- Azure DevOps
- AWS CodePipeline
- Google Cloud Build

---

## Execution Workflow

### Phase 1: Requirements Analysis

**Step 1.1: Understand the Project**

```
Gather:
- What language/framework? (Node, Python, Go, etc.)
- What package manager? (npm, pip, cargo, etc.)
- What testing framework?
- Deployment target? (AWS, GCP, Vercel, Docker, K8s)
- Branch strategy? (main only, GitFlow, trunk-based)
- Any secrets/credentials needed?
```

**Step 1.2: Define Pipeline Stages**

| Stage | Purpose | Typical Jobs |
|-------|---------|--------------|
| **Lint** | Code quality | ESLint, Flake8, Prettier |
| **Test** | Correctness | Unit, integration, E2E |
| **Build** | Artifact creation | Compile, bundle, Docker |
| **Security** | Vulnerability scan | SAST, dependency audit |
| **Deploy** | Release | Staging, production |

---

### Phase 2: GitHub Actions

**Step 2.1: Basic Workflow Structure**

```yaml
# .github/workflows/ci.yml
name: CI

on:
  push:
    branches: [main, develop]
  pull_request:
    branches: [main]

# Cancel in-progress runs for same branch
concurrency:
  group: ${{ github.workflow }}-${{ github.ref }}
  cancel-in-progress: true

jobs:
  lint:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Setup Node
        uses: actions/setup-node@v4
        with:
          node-version: '20'
          cache: 'npm'
      - run: npm ci
      - run: npm run lint

  test:
    runs-on: ubuntu-latest
    needs: lint  # Run after lint passes
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: '20'
          cache: 'npm'
      - run: npm ci
      - run: npm test -- --coverage
      - name: Upload coverage
        uses: codecov/codecov-action@v3

  build:
    runs-on: ubuntu-latest
    needs: test
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: '20'
          cache: 'npm'
      - run: npm ci
      - run: npm run build
      - name: Upload artifact
        uses: actions/upload-artifact@v4
        with:
          name: build
          path: dist/
```

**Step 2.2: Matrix Builds (Multi-Version Testing)**

```yaml
jobs:
  test:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        node-version: [18, 20, 22]
        os: [ubuntu-latest, windows-latest]
      fail-fast: false  # Continue other jobs if one fails
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: ${{ matrix.node-version }}
      - run: npm ci
      - run: npm test
```

**Step 2.3: Caching Dependencies**

```yaml
# Node.js
- uses: actions/setup-node@v4
  with:
    node-version: '20'
    cache: 'npm'  # Built-in caching

# Python
- uses: actions/setup-python@v5
  with:
    python-version: '3.11'
    cache: 'pip'

# Custom cache
- uses: actions/cache@v4
  with:
    path: ~/.cache/custom
    key: ${{ runner.os }}-custom-${{ hashFiles('**/lockfile') }}
    restore-keys: |
      ${{ runner.os }}-custom-
```

**Step 2.4: Secrets and Environment Variables**

```yaml
jobs:
  deploy:
    runs-on: ubuntu-latest
    environment: production  # Use GitHub environment
    env:
      NODE_ENV: production
    steps:
      - name: Deploy
        env:
          AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
          AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
        run: |
          aws s3 sync dist/ s3://my-bucket
```

**Step 2.5: Conditional Execution**

```yaml
jobs:
  deploy:
    runs-on: ubuntu-latest
    # Only run on main branch, not PRs
    if: github.ref == 'refs/heads/main' && github.event_name == 'push'
    steps:
      - name: Deploy to production
        run: ./deploy.sh

  # Skip if commit message contains [skip ci]
  test:
    if: "!contains(github.event.head_commit.message, '[skip ci]')"
```

**Step 2.6: Reusable Workflows**

```yaml
# .github/workflows/reusable-build.yml
name: Reusable Build

on:
  workflow_call:
    inputs:
      node-version:
        required: true
        type: string
    secrets:
      npm-token:
        required: true

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: ${{ inputs.node-version }}
      - run: npm ci
        env:
          NPM_TOKEN: ${{ secrets.npm-token }}
      - run: npm run build
```

```yaml
# .github/workflows/ci.yml (calling reusable workflow)
jobs:
  build:
    uses: ./.github/workflows/reusable-build.yml
    with:
      node-version: '20'
    secrets:
      npm-token: ${{ secrets.NPM_TOKEN }}
```

**Step 2.7: Complete Production Workflow**

```yaml
name: Production CI/CD

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

concurrency:
  group: ${{ github.workflow }}-${{ github.ref }}
  cancel-in-progress: true

env:
  NODE_VERSION: '20'

jobs:
  # ============ Quality Checks ============
  lint:
    name: Lint & Format
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: ${{ env.NODE_VERSION }}
          cache: 'npm'
      - run: npm ci
      - run: npm run lint
      - run: npm run format:check

  typecheck:
    name: Type Check
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: ${{ env.NODE_VERSION }}
          cache: 'npm'
      - run: npm ci
      - run: npm run typecheck

  # ============ Testing ============
  test:
    name: Unit Tests
    runs-on: ubuntu-latest
    needs: [lint, typecheck]
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: ${{ env.NODE_VERSION }}
          cache: 'npm'
      - run: npm ci
      - run: npm test -- --coverage
      - uses: codecov/codecov-action@v3
        with:
          fail_ci_if_error: true

  e2e:
    name: E2E Tests
    runs-on: ubuntu-latest
    needs: [lint, typecheck]
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: ${{ env.NODE_VERSION }}
          cache: 'npm'
      - run: npm ci
      - run: npx playwright install --with-deps
      - run: npm run test:e2e

  # ============ Security ============
  security:
    name: Security Scan
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: npm audit --audit-level=high
      - uses: github/codeql-action/init@v3
        with:
          languages: javascript
      - uses: github/codeql-action/analyze@v3

  # ============ Build ============
  build:
    name: Build
    runs-on: ubuntu-latest
    needs: [test, e2e, security]
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: ${{ env.NODE_VERSION }}
          cache: 'npm'
      - run: npm ci
      - run: npm run build
      - uses: actions/upload-artifact@v4
        with:
          name: build-${{ github.sha }}
          path: dist/
          retention-days: 7

  # ============ Deploy ============
  deploy-staging:
    name: Deploy Staging
    runs-on: ubuntu-latest
    needs: build
    if: github.event_name == 'pull_request'
    environment:
      name: staging
      url: https://staging.example.com
    steps:
      - uses: actions/download-artifact@v4
        with:
          name: build-${{ github.sha }}
          path: dist/
      - name: Deploy to staging
        run: echo "Deploy to staging server"

  deploy-production:
    name: Deploy Production
    runs-on: ubuntu-latest
    needs: build
    if: github.ref == 'refs/heads/main' && github.event_name == 'push'
    environment:
      name: production
      url: https://example.com
    steps:
      - uses: actions/download-artifact@v4
        with:
          name: build-${{ github.sha }}
          path: dist/
      - name: Deploy to production
        run: echo "Deploy to production server"
```

---

### Phase 3: GitLab CI/CD

**Step 3.1: Basic Pipeline**

```yaml
# .gitlab-ci.yml
stages:
  - lint
  - test
  - build
  - deploy

variables:
  NODE_VERSION: "20"

default:
  image: node:${NODE_VERSION}
  cache:
    key: ${CI_COMMIT_REF_SLUG}
    paths:
      - node_modules/

lint:
  stage: lint
  script:
    - npm ci
    - npm run lint

test:
  stage: test
  script:
    - npm ci
    - npm test -- --coverage
  coverage: '/All files[^|]*\|[^|]*\s+([\d\.]+)/'
  artifacts:
    reports:
      coverage_report:
        coverage_format: cobertura
        path: coverage/cobertura-coverage.xml

build:
  stage: build
  script:
    - npm ci
    - npm run build
  artifacts:
    paths:
      - dist/
    expire_in: 1 week

deploy_staging:
  stage: deploy
  script:
    - echo "Deploy to staging"
  environment:
    name: staging
    url: https://staging.example.com
  rules:
    - if: $CI_MERGE_REQUEST_ID

deploy_production:
  stage: deploy
  script:
    - echo "Deploy to production"
  environment:
    name: production
    url: https://example.com
  rules:
    - if: $CI_COMMIT_BRANCH == "main"
  when: manual  # Require manual approval
```

**Step 3.2: GitLab-Specific Features**

```yaml
# Include templates
include:
  - template: Security/SAST.gitlab-ci.yml
  - template: Security/Dependency-Scanning.gitlab-ci.yml

# Parallel jobs
test:
  parallel: 3
  script:
    - npm test -- --shard=$CI_NODE_INDEX/$CI_NODE_TOTAL

# Services (databases, etc.)
test:
  services:
    - postgres:15
  variables:
    POSTGRES_DB: test
    DATABASE_URL: postgres://postgres@postgres/test
```

---

### Phase 4: Jenkins

**Step 4.1: Jenkinsfile (Declarative)**

```groovy
// Jenkinsfile
pipeline {
    agent any

    environment {
        NODE_VERSION = '20'
        NPM_CONFIG_CACHE = "${WORKSPACE}/.npm"
    }

    options {
        buildDiscarder(logRotator(numToKeepStr: '10'))
        timeout(time: 30, unit: 'MINUTES')
        disableConcurrentBuilds()
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install') {
            steps {
                sh 'npm ci'
            }
        }

        stage('Lint') {
            steps {
                sh 'npm run lint'
            }
        }

        stage('Test') {
            steps {
                sh 'npm test -- --coverage'
            }
            post {
                always {
                    junit 'coverage/junit.xml'
                    publishHTML([
                        reportDir: 'coverage/lcov-report',
                        reportFiles: 'index.html',
                        reportName: 'Coverage Report'
                    ])
                }
            }
        }

        stage('Build') {
            steps {
                sh 'npm run build'
            }
        }

        stage('Deploy Staging') {
            when {
                branch 'develop'
            }
            steps {
                sh './deploy.sh staging'
            }
        }

        stage('Deploy Production') {
            when {
                branch 'main'
            }
            input {
                message "Deploy to production?"
                ok "Deploy"
            }
            steps {
                sh './deploy.sh production'
            }
        }
    }

    post {
        success {
            slackSend color: 'good', message: "Build succeeded: ${env.JOB_NAME} #${env.BUILD_NUMBER}"
        }
        failure {
            slackSend color: 'danger', message: "Build failed: ${env.JOB_NAME} #${env.BUILD_NUMBER}"
        }
    }
}
```

---

### Phase 5: Docker & Containerized Builds

**Step 5.1: Docker Build in CI**

```yaml
# GitHub Actions
jobs:
  docker:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Set up Docker Buildx
        uses: docker/setup-buildx-action@v3

      - name: Login to Container Registry
        uses: docker/login-action@v3
        with:
          registry: ghcr.io
          username: ${{ github.actor }}
          password: ${{ secrets.GITHUB_TOKEN }}

      - name: Build and push
        uses: docker/build-push-action@v5
        with:
          context: .
          push: ${{ github.event_name != 'pull_request' }}
          tags: |
            ghcr.io/${{ github.repository }}:${{ github.sha }}
            ghcr.io/${{ github.repository }}:latest
          cache-from: type=gha
          cache-to: type=gha,mode=max
```

**Step 5.2: Multi-Stage Dockerfile**

```dockerfile
# Dockerfile
# Build stage
FROM node:20-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
RUN npm run build

# Production stage
FROM node:20-alpine AS production
WORKDIR /app
COPY --from=builder /app/dist ./dist
COPY --from=builder /app/node_modules ./node_modules
EXPOSE 3000
CMD ["node", "dist/index.js"]
```

---

### Phase 6: Common Patterns

**Pattern 1: Monorepo (Turborepo/Nx)**

```yaml
# GitHub Actions for monorepo
jobs:
  changes:
    runs-on: ubuntu-latest
    outputs:
      packages: ${{ steps.filter.outputs.changes }}
    steps:
      - uses: actions/checkout@v4
      - uses: dorny/paths-filter@v3
        id: filter
        with:
          filters: |
            api:
              - 'packages/api/**'
            web:
              - 'packages/web/**'

  build:
    needs: changes
    if: needs.changes.outputs.packages != '[]'
    strategy:
      matrix:
        package: ${{ fromJson(needs.changes.outputs.packages) }}
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: npm ci
      - run: npx turbo build --filter=${{ matrix.package }}
```

**Pattern 2: Scheduled Jobs**

```yaml
on:
  schedule:
    - cron: '0 0 * * *'  # Daily at midnight UTC
  workflow_dispatch:  # Allow manual trigger

jobs:
  nightly:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: npm ci
      - run: npm run test:full
      - run: npm audit
```

**Pattern 3: Release Automation**

```yaml
on:
  push:
    tags:
      - 'v*'

jobs:
  release:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: '20'
          registry-url: 'https://registry.npmjs.org'
      - run: npm ci
      - run: npm run build
      - run: npm publish
        env:
          NODE_AUTH_TOKEN: ${{ secrets.NPM_TOKEN }}

      - name: Create GitHub Release
        uses: softprops/action-gh-release@v1
        with:
          generate_release_notes: true
```

---

### Phase 7: Optimization Strategies

**Speed Optimization:**

```yaml
# 1. Parallel jobs
jobs:
  lint:
    ...
  test:
    ...
  # lint and test run in parallel by default

# 2. Caching
- uses: actions/cache@v4
  with:
    path: node_modules
    key: ${{ runner.os }}-node-${{ hashFiles('package-lock.json') }}

# 3. Skip unnecessary runs
if: "!contains(github.event.head_commit.message, '[skip ci]')"

# 4. Cancel in-progress runs
concurrency:
  group: ${{ github.workflow }}-${{ github.ref }}
  cancel-in-progress: true

# 5. Use larger runners (GitHub)
runs-on: ubuntu-latest-4-cores
```

**Cost Optimization:**

```yaml
# 1. Use pull_request for PRs (doesn't trigger on fork PRs by default)
on:
  pull_request:
    branches: [main]

# 2. Path filters
on:
  push:
    paths:
      - 'src/**'
      - 'package*.json'

# 3. Timeout limits
jobs:
  test:
    timeout-minutes: 10
```

---

## Quality Checklist

### Pipeline Design
- [ ] All stages defined (lint, test, build, deploy)
- [ ] Caching configured for dependencies
- [ ] Artifacts uploaded for debugging
- [ ] Secrets stored securely (not in code)
- [ ] Environment variables documented

### Reliability
- [ ] Concurrency controls in place
- [ ] Timeouts set appropriately
- [ ] Retry logic for flaky operations
- [ ] Notifications on failure

### Security
- [ ] Secrets rotated regularly
- [ ] Minimal permissions (principle of least privilege)
- [ ] Dependency scanning enabled
- [ ] SAST/DAST configured

---

## Integration with Other Skills

### With security-audit-assistant:
- Add security scanning stages
- Configure SAST/DAST tools

### With test-case-generator:
- Ensure tests are CI-compatible
- Configure test reporting

### With code-review-assistant:
- Add automated code quality checks
- Configure linting in CI

---

## Troubleshooting

### Build fails intermittently
- Check for race conditions
- Add retry logic
- Review resource limits

### Cache not working
- Verify cache key includes lockfile hash
- Check cache size limits
- Clear cache and rebuild

### Slow builds
- Enable parallelization
- Optimize Docker layers
- Use incremental builds

---

## Version History

- v1.0.0 (2025-12-07): Initial release with GitHub Actions, GitLab CI, Jenkins patterns, Docker integration, and optimization strategies
