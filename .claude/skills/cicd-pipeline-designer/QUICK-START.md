# CI/CD Pipeline Designer - Quick Start

## Request a Pipeline

```
Create a [GitHub Actions/GitLab CI] pipeline for:
- Language: [Node/Python/Go]
- Tests: [Jest/pytest/go test]
- Deploy to: [Vercel/AWS/Docker]
```

---

## GitHub Actions Template

```yaml
# .github/workflows/ci.yml
name: CI

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: '20'
          cache: 'npm'
      - run: npm ci
      - run: npm test
      - run: npm run build
```

---

## GitLab CI Template

```yaml
# .gitlab-ci.yml
stages:
  - test
  - build
  - deploy

test:
  stage: test
  image: node:20
  script:
    - npm ci
    - npm test

build:
  stage: build
  script:
    - npm run build
  artifacts:
    paths:
      - dist/
```

---

## Common Patterns

**Cache dependencies:**
```yaml
- uses: actions/setup-node@v4
  with:
    cache: 'npm'
```

**Run on specific paths:**
```yaml
on:
  push:
    paths:
      - 'src/**'
```

**Matrix builds:**
```yaml
strategy:
  matrix:
    node: [18, 20, 22]
```

**Deploy on main only:**
```yaml
if: github.ref == 'refs/heads/main'
```

---

## Stage Order

```
lint → test → build → security → deploy
  ↓      ↓      ↓        ↓         ↓
 fast   unit  artifact  scan    staging
       integration           production
```

---

## Secrets

**GitHub Actions:**
```yaml
env:
  API_KEY: ${{ secrets.API_KEY }}
```

**GitLab CI:**
```yaml
variables:
  API_KEY: $API_KEY  # Set in CI/CD settings
```

---

## Speed Tips

| Tip | Implementation |
|-----|----------------|
| Cache deps | `cache: 'npm'` in setup action |
| Parallel jobs | Remove `needs:` between independent jobs |
| Cancel old runs | `concurrency: cancel-in-progress: true` |
| Skip CI | Add `[skip ci]` to commit message |

---

## Checklist

- [ ] Checkout step included
- [ ] Dependencies cached
- [ ] Tests run with coverage
- [ ] Artifacts uploaded
- [ ] Secrets not hardcoded
- [ ] Deploy only on main
