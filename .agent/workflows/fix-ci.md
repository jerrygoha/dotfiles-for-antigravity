---
description: Diagnose and fix CI/CD pipeline failures
---

# Fix CI Workflow

Systematic approach with environment verification.

---

## 1. Identify Failure

// turbo
```bash
gh run list --limit 5
```

**Categorize:**

| Category | Common Causes | Quick Check |
|----------|---------------|-------------|
| Build | Missing deps, syntax | `npm ci && npm run build` |
| Lint | Style violations | `npm run lint` |
| Test | Failing assertions | `npm test` |
| Deploy | Config, secrets | Check env vars |
| Timeout | Slow tests | Optimize/increase |

---

## 2. Reproduce Locally (CRITICAL)

**Environment Parity Check:**

// turbo
```bash
# Compare local vs CI environment
echo "Node: $(node -v)"
echo "npm: $(npm -v)"
cat .nvmrc 2>/dev/null || echo "No .nvmrc"
```

// turbo
```bash
# Match CI environment
rm -rf node_modules
npm ci
npm run lint
npm run test
npm run build
```

> ⚠️ 로컬에서 재현되지 않으면 환경 차이 문제일 가능성 높음

---

## 3. Common Solutions

**Build Failures:**
```bash
rm -rf node_modules package-lock.json
npm install
```

**Flaky Tests:**
- Add retry logic
- Check race conditions
- Mock external dependencies properly

**Environment Variables:**
// turbo
```bash
grep -r "process.env" --include="*.ts" --include="*.js" | grep -v node_modules | head -10
```

---

## 4. Verify Fix

// turbo
```bash
npm run lint && npm run test && npm run build
```

---

## 5. Push & Monitor

```bash
git add .
git commit -m "fix(ci): [description]"
git push
```

// turbo
```bash
gh run watch
```

---

## Prevention

- [ ] Run full suite before push
- [ ] Keep dependencies updated
- [ ] Use lock files
- [ ] Document required env vars
