---
description: Systematic debugging using four-phase root cause analysis
---

# Debug Workflow

Use this systematic approach to find the root cause before attempting any fixes.

## Four-Phase Process

### Phase 1: Reproduce & Observe

1. **Reproduce the issue**
   - Get exact steps to reproduce
   - Note any environment-specific conditions
   - Capture error messages verbatim

2. **Gather evidence**
   ```bash
   # Check relevant logs
   tail -100 /path/to/logs
   
   # Check system state
   ps aux | grep [process]
   ```

3. **Document observations**
   - What happens vs what should happen
   - When did it start occurring?
   - Is it consistent or intermittent?

### Phase 2: Hypothesize

1. List possible causes (minimum 3):
   - [ ] Hypothesis 1: ...
   - [ ] Hypothesis 2: ...
   - [ ] Hypothesis 3: ...

2. Rank by likelihood:
   - Most likely first
   - Consider recent changes

### Phase 3: Test Hypotheses

1. Design minimal tests for each hypothesis
2. Test one variable at a time
3. Document results:

```markdown
| Hypothesis | Test | Result | Conclusion |
|------------|------|--------|------------|
| H1: Cache miss | Clear cache, retry | Still fails | ❌ Ruled out |
| H2: Race condition | Add delay | Works | ✅ Likely cause |
```

### Phase 4: Fix & Verify

1. Implement the fix for confirmed root cause
2. Verify the fix:
   - [ ] Issue no longer reproduces
   - [ ] No regression in related functionality
   - [ ] Tests pass

3. Document the resolution:
   ```markdown
   ## Root Cause
   [Description]

   ## Fix Applied
   [What was changed]

   ## Prevention
   [How to prevent recurrence]
   ```

## Anti-Patterns to Avoid

❌ **Don't** make random changes hoping something works  
❌ **Don't** fix symptoms without understanding root cause  
❌ **Don't** skip the hypothesis phase  
✅ **Do** follow the process systematically
