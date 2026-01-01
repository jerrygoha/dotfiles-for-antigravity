---
description: Execute implementation plan in batches with review checkpoints
---

# Execute Plan Workflow

Systematically work through an implementation plan with checkpoints.

## Prerequisites

- Have an existing plan (use `/write-plan` first if needed)
- User has approved the plan

## Process

### 1. Load the Plan

```bash
# Find and read the plan
cat .agent/plans/*.md
```

### 2. Execute in Batches

Work through tasks in logical groups:

```markdown
## Current Batch: Phase 1

### Executing:
- [x] Step 1.1: Create database schema
- [ ] Step 1.2: Implement model layer
- [ ] Step 1.3: Add validation

### Progress: 1/3 complete
```

### 3. Checkpoint After Each Phase

After completing a batch:

1. **Summarize what was done**
   - Files created/modified
   - Key decisions made

2. **Verify status**
   - Build passes?
   - Tests pass?

3. **Ask to continue**
   ```
   Phase 1 complete. Ready for Phase 2?
   - Next: Implement API endpoints
   - Estimated time: 2 hours
   ```

### 4. Handle Blockers

If you encounter issues:

1. Document the blocker
2. Assess impact on plan
3. Propose alternatives:
   ```markdown
   ## Blocker Encountered
   
   **Issue**: [Description]
   
   **Options**:
   1. [Workaround A] - Pros/Cons
   2. [Workaround B] - Pros/Cons
   3. Skip and revisit later
   
   **Recommendation**: [Your suggestion]
   ```

### 5. Completion

When all phases are done:

1. Update plan with completion status
2. Run final verification:
   ```bash
   # Build check
   npm run build
   
   # Test check
   npm test
   ```

3. Create summary:
   ```markdown
   ## Execution Complete
   
   ### Completed Tasks
   - [x] Phase 1: Database layer
   - [x] Phase 2: API endpoints
   - [x] Phase 3: Frontend integration
   
   ### Key Changes
   - Created 5 new files
   - Modified 3 existing files
   
   ### Next Steps
   - Code review
   - Deploy to staging
   ```

## Best Practices

- ✅ Complete one batch before starting next
- ✅ Always run checks between phases
- ✅ Keep user informed of progress
- ❌ Don't skip ahead in the plan
- ❌ Don't make changes outside the plan scope
