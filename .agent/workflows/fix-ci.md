---
description: Diagnose and fix CI/CD pipeline failures
---

# Fix CI Workflow

Systematic approach to troubleshoot and resolve CI/CD failures.

## Process

### 1. Identify the Failure

// turbo
```bash
# Check recent CI runs (if using GitHub Actions)
gh run list --limit 5
```

Read the CI logs to identify:
- Which step failed?
- What error message?
- Is it flaky or consistent?

### 2. Categorize the Failure

| Category | Common Causes | Quick Fix |
|----------|---------------|-----------|
| **Build** | Missing deps, syntax errors | Check package.json, fix errors |
| **Lint** | Style violations | Run linter locally, fix issues |
| **Test** | Failing assertions | Debug test, check for flaky tests |
| **Deploy** | Config issues, secrets | Verify environment variables |
| **Timeout** | Slow tests, infinite loops | Optimize or increase timeout |

### 3. Reproduce Locally

// turbo
```bash
# Match CI environment locally
npm ci
npm run lint
npm run test
npm run build
```

### 4. Common Solutions

#### Build Failures
```bash
# Clear node_modules and reinstall
rm -rf node_modules package-lock.json
npm install
```

#### Lock File Issues
```bash
# Regenerate lock file
npm install --package-lock-only
```

#### Flaky Tests
- Add retry logic
- Check for race conditions
- Mock external dependencies

#### Missing Environment Variables
```bash
# Verify all required env vars are set
grep -r "process.env" --include="*.ts" --include="*.js"
```

### 5. Verify Fix

// turbo
```bash
# Run full CI check locally
npm run lint && npm run test && npm run build
```

### 6. Push and Monitor

```bash
git add .
git commit -m "fix(ci): [description of fix]"
git push
```

Then monitor the CI pipeline to confirm the fix.

## Prevention Checklist

- [ ] Run full test suite before pushing
- [ ] Keep dependencies up to date
- [ ] Use lock files consistently
- [ ] Set appropriate timeouts
- [ ] Document required environment variables
