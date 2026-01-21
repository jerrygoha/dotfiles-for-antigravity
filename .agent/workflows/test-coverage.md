---
description: Analyze test coverage and add tests to reach 80%+ threshold
---

# Test Coverage Workflow

Analyze current test coverage and generate tests for under-covered files.

## When to Use

- Pre-commit coverage check
- CI coverage requirement
- New feature coverage verification
- Coverage improvement sprint

---

## Process

### 1. Generate Coverage Report

// turbo
```bash
npm test -- --coverage 2>/dev/null || npm run test:coverage
```

### 2. Identify Under-Covered Files

Focus on files below 80% coverage:

| Priority | Coverage | Action |
|----------|----------|--------|
| Critical | < 50% | Immediate attention |
| High | 50-70% | Add tests this sprint |
| Medium | 70-80% | Improve soon |
| OK | > 80% | Maintain |

### 3. Coverage Requirements by Module

| Module Type | Line | Branch | Rationale |
|-------------|------|--------|-----------|
| Core/Critical | 90%+ | 85%+ | Business critical |
| Business Logic | 80%+ | 75%+ | Standard |
| Utilities | 100% | 100% | Simple, testable |
| UI Components | 70%+ | 60%+ | Complex to test |

### 4. Generate Missing Tests

For each under-covered file:

1. Identify uncovered lines/branches
2. Write focused test cases
3. Cover edge cases and error paths
4. Verify coverage increase

### 5. Verify Improvement

// turbo
```bash
npm test -- --coverage --coverageReporters=text-summary
```

---

## Coverage Report Format

```markdown
## Coverage Analysis

### Before → After
| Metric | Before | After | Target |
|--------|--------|-------|--------|
| Statements | 72% | 85% | 80% ✅ |
| Branches | 65% | 82% | 80% ✅ |
| Functions | 70% | 88% | 80% ✅ |

### Tests Added
- `src/api/auth.test.ts` - 3 test cases
- `src/utils/calc.test.ts` - 5 test cases
```

---

## Best Practices

- ✅ Focus on branch coverage, not just lines
- ✅ Test error paths and edge cases
- ✅ Write meaningful assertions
- ✅ Use test factories for consistent data
- ❌ Don't write tests just for numbers
- ❌ Don't mock too much (integration value)

---

## Related Workflows

- `/tdd` - Write new code with tests first
- `/testing` - Advanced testing techniques
