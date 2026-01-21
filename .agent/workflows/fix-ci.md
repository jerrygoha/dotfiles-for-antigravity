---
description: Diagnose and fix CI/CD pipeline failures
---

# Fix CI Workflow

Systematic approach to diagnose and fix CI/CD failures with local reproduction.

---

## Process

### 1. Identify Failure

// turbo
```bash
gh run list --limit 5 2>/dev/null || echo "gh CLI not available"
```

**Failure Categories:**

| Category | Common Causes | Quick Check |
|----------|---------------|-------------|
| Build | Missing deps, syntax | `npm ci && npm run build` |
| Lint | Style violations | `npm run lint` |
| Test | Failing assertions | `npm test` |
| Deploy | Config, secrets | Check env vars |
| Timeout | Slow tests | Optimize or increase limit |

### 2. Reproduce Locally (CRITICAL)

> ⚠️ If it doesn't reproduce locally, it's likely an environment issue.

**Environment Parity Check:**

// turbo
```bash
echo "Node: $(node -v)"
echo "npm: $(npm -v)"
cat .nvmrc 2>/dev/null || echo "No .nvmrc"
```

**Match CI Environment:**

// turbo
```bash
rm -rf node_modules
npm ci
npm run lint
npm test
npm run build
```

### 3. Common Solutions

**Build Failures:**
```bash
rm -rf node_modules package-lock.json
npm install
```

**Flaky Tests:**
- Add retry logic
- Check race conditions
- Properly mock external dependencies
- Check for time-dependent tests

**Environment Variables:**

// turbo
```bash
grep -r "process.env" --include="*.ts" --include="*.js" | grep -v node_modules | head -10
```

### 4. Apply Fix

// turbo
```bash
npm run lint && npm test && npm run build
```

### 5. Push & Monitor

```bash
git add .
git commit -m "fix(ci): [description]"
git push
```

// turbo
```bash
gh run watch 2>/dev/null || echo "Monitor CI in browser"
```

---

## Common CI Issues

| Issue | Symptom | Solution |
|-------|---------|----------|
| Node version mismatch | Build fails only in CI | Set `.nvmrc` and CI config |
| Missing env vars | `undefined` errors | Add to CI secrets |
| Lock file mismatch | Dependency errors | Regenerate `package-lock.json` |
| Flaky tests | Random failures | Add retries, fix race conditions |
| Memory limits | OOM errors | Increase CI memory or optimize |

---

## Prevention Checklist

- [ ] Run full test suite before push
- [ ] Keep dependencies updated
- [ ] Use lock files (`package-lock.json`)
- [ ] Document required environment variables
- [ ] Match local Node version with CI

---

## Related Workflows

- `/testing` - Add missing tests
- `/code-review` - Review fix before push
