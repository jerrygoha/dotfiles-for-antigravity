---
description: TDD-based systematic debugging with evidence-driven root cause analysis
---

# Debug Workflow

Evidence-based debugging using Test-Driven approach. **Never fix based on assumptions alone.**

## Core Principle

> ❌ "This might be the cause" → Fix  
> ✅ "Test reproduces bug → Cause confirmed → Fix → Test passes"

---

## When to Use

- Bug reported by users
- Intermittent failures
- Multiple possible causes
- Complex logic errors
- Reproducing edge cases

---

## Six-Phase Process

### Phase 0: Reproduction Test (MANDATORY)

**Write a failing test BEFORE fixing anything.**

```javascript
describe('BUG-123: Login session missing', () => {
  it('should reproduce the reported issue', () => {
    const result = login(user);
    expect(result.session).toBeDefined(); // Currently FAILS
  });
});
```

// turbo
```bash
# Run reproduction test - MUST FAIL
npm test -- --testPathPattern="BUG-123"
```

**Checkpoint:**
- [ ] Test accurately reproduces bug conditions?
- [ ] Test currently FAILS?
- [ ] When fixed, test PASS = bug resolved?

---

### Phase 1: Evidence Collection

**Collect runtime data, not assumptions.**

// turbo
```bash
# Collect evidence
grep -E "(Error|Exception|FAIL)" logs/*.log | tail -20
```

**Evidence Checklist:**

| Evidence Type | Source | Collected? |
|--------------|--------|------------|
| Error stack trace | Console/Logs | [ ] |
| Input data | Reproduction case | [ ] |
| System state | Env vars, config | [ ] |
| Timeline | When did it start? | [ ] |

---

### Phase 2: Hypothesis Formation (Minimum 3)

| # | Hypothesis | Evidence | Verification Method |
|---|-----------|----------|---------------------|
| H1 | Race condition | Stack trace shows Promise rejection | Add delay test |
| H2 | Null from API | Error only with empty response | Mock empty response |
| H3 | Cache stale | Works after cache clear | Test with/without cache |

> ⚠️ **Anti-Pattern**: Don't form hypotheses without evidence

---

### Phase 3: Test-Driven Verification

**Verify each hypothesis with tests:**

```javascript
// H1 verification: Race condition test
describe('H1: Race condition hypothesis', () => {
  it('should handle concurrent requests', async () => {
    const results = await Promise.all([
      handler(request1),
      handler(request2),
    ]);
    expect(results).toEqual([expected1, expected2]);
  });
});
```

**Verification Matrix:**

| Hypothesis | Test Written | Result | Conclusion |
|-----------|-------------|--------|------------|
| H1 | `h1.test.js` | FAIL | ✅ Root cause found |
| H2 | `h2.test.js` | PASS | ❌ Eliminated |
| H3 | `h3.test.js` | PASS | ❌ Eliminated |

---

### Phase 4: Fix Implementation

**Only fix the CONFIRMED cause.**

```markdown
## Fix Strategy

**Root Cause**: [Confirmed in Phase 3]
**Evidence**: [Test results and logs]

### Changes:
1. [File]: [Change description]
2. [File]: [Change description]
```

---

### Phase 5: Verification & Regression

// turbo
```bash
# 1. Reproduction test must PASS now
npm test -- --testPathPattern="BUG-123"

# 2. Full regression test
npm test
```

**Final Checklist:**
- [ ] Phase 0 reproduction test PASSES?
- [ ] All existing tests PASS?
- [ ] No new regressions?

---

### Phase 6: Documentation

```markdown
## Bug Resolution Report

**Issue**: [Description]
**Root Cause**: [Evidence-backed cause]
**Evidence**: Test `[file]` confirmed hypothesis H1
**Fix Applied**: [Changes made]
**Prevention**: [How to prevent recurrence]
```

---

## Anti-Patterns

| ❌ Don't | ✅ Do |
|---------|------|
| Fix based on assumptions | Confirm with tests first |
| "Maybe this is the issue" | "This test fails, confirming cause" |
| Fix multiple hypotheses at once | Verify one at a time |
| Manual verification only | Automated test verification |

---

## Related Workflows

- `/tdd` - For new features (not bugs)
- `/testing` - Add comprehensive tests
- `/learn` - Save pattern after complex fix
