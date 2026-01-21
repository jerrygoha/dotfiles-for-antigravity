---
description: Code review checklist for quality and security
---

# Code Review Workflow

Security and quality review before commit/PR.

## When to Use

- Before committing changes
- Before creating PR
- Security audit
- Pre-team review self-check

---

## Process

### 1. Check Staged Changes

// turbo
```bash
git diff --cached --stat 2>/dev/null || git diff --stat
```

### 2. Security Review (CRITICAL)

| Check | Command/Action |
|-------|---------------|
| Hardcoded secrets | `grep -rn "password\|api_key\|secret" src/` |
| SQL injection | Check for string concatenation in queries |
| XSS vulnerability | Check for `dangerouslySetInnerHTML`, unescaped output |
| Auth bypass | Verify all routes check authorization |

### 3. Code Quality Review

**Critical Issues (Block commit):**
- [ ] No hardcoded secrets
- [ ] No SQL/XSS vulnerabilities
- [ ] All inputs validated
- [ ] Proper error handling

**High Priority:**
- [ ] Functions < 50 lines
- [ ] Files < 800 lines
- [ ] Nesting depth < 4 levels
- [ ] No `console.log` in production code
- [ ] No TODO/FIXME without issue reference

**Medium Priority:**
- [ ] Immutable patterns used
- [ ] Proper TypeScript types (no `any`)
- [ ] Tests added for new code
- [ ] Accessibility considered

### 4. Generate Review Report

```markdown
## Code Review Report

### 🔴 CRITICAL (Must fix before commit)
- [File:Line] Issue description

### 🟠 HIGH (Should fix)
- [File:Line] Issue description

### 🟡 MEDIUM (Recommended)
- [File:Line] Issue description

### Summary
- CRITICAL: X
- HIGH: X
- MEDIUM: X

**Verdict**: [APPROVE / REQUEST CHANGES]
```

---

## Security Checklist

```
[ ] No hardcoded secrets (API keys, passwords, tokens)
[ ] SQL injection prevented (parameterized queries)
[ ] XSS prevented (sanitized output)
[ ] CSRF protection enabled
[ ] Input validation on all user inputs
[ ] Error messages don't leak sensitive info
[ ] Rate limiting considered
[ ] Authentication/authorization verified
```

---

## Best Practices

- ✅ Run frequently (small batches)
- ✅ Fix CRITICAL issues immediately
- ✅ Automate with pre-commit hooks
- ❌ Never commit with CRITICAL issues
- ❌ Don't skip security checks

---

## Related Workflows

- `/create-pr` - After review passes
- `/testing` - Ensure test coverage
