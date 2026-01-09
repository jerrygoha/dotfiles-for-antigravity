---
description: Code review checklist for quality and security
---

# Code Review Workflow

Systematic review with verification commands.

---

## Pre-Review Verification

// turbo
```bash
npm run build && npm run lint && npm test
```

- [ ] Build passes
- [ ] No lint errors
- [ ] Tests pass
- [ ] Branch up-to-date with main

---

## Code Quality

### 1. Readability
- [ ] Clear variable/function names
- [ ] Comments for complex logic only
- [ ] Consistent style
- [ ] No dead code

### 2. Architecture
- [ ] SOLID principles followed
- [ ] DRY - no duplication
- [ ] KISS - simple solutions
- [ ] Proper separation of concerns

### 3. Error Handling
- [ ] All errors caught and handled
- [ ] User-friendly error messages
- [ ] Appropriate logging

---

## Security Audit

// turbo
```bash
# Check for secrets
git diff origin/main | grep -iE "(password|secret|api_key|token)" || echo "No secrets found"

# Check dependencies
npm audit
```

**OWASP Quick Check:**

| Risk | Check | Verified |
|------|-------|----------|
| Injection | Parameterized queries? | [ ] |
| XSS | Output encoded? | [ ] |
| Auth | Proper session handling? | [ ] |
| Secrets | No hardcoded credentials? | [ ] |
| Access | Authorization checks? | [ ] |

---

## Performance

// turbo
```bash
# Check for N+1 queries (if applicable)
grep -rn "\.find\|\.query" --include="*.ts" --include="*.js" | head -20
```

- [ ] No N+1 query problems
- [ ] Appropriate caching
- [ ] Efficient algorithms
- [ ] No memory leaks
- [ ] Lazy loading where needed

---

## Final Steps

1. Provide constructive feedback
2. Approve or request changes
3. Follow up on requested changes
