---
description: Execute implementation plan in batches with review checkpoints
---

# Execute Plan Workflow

Work through plans with verification at each phase.

---

## Prerequisites

- Approved plan exists (use `/write-plan` first)
- User has reviewed and approved

---

## Process

### 1. Load Plan

// turbo
```bash
ls -la .agent/plans/*.md 2>/dev/null || echo "No plans found"
```

### 2. Execute in Batches

```markdown
## Current Batch: Phase 1

### Executing:
- [x] Step 1.1: Create schema
- [ ] Step 1.2: Implement model
- [ ] Step 1.3: Add validation

### Progress: 1/3
```

### 3. Checkpoint After Each Phase

**Verification Steps:**

// turbo
```bash
npm run build && npm test
```

**Report Template:**
```markdown
## Phase [N] Complete

**Done:**
- [Changes made]

**Verified:**
- Build: ✅/❌
- Tests: ✅/❌

**Next:** Phase [N+1] - [Description]
Continue? [Y/N]
```

### 4. Handle Blockers

```markdown
## Blocker Encountered

**Issue**: [Description]
**Impact**: [High/Med/Low]

**Options**:
1. [Workaround A] - [Pros/Cons]
2. [Workaround B] - [Pros/Cons]
3. Skip and revisit

**Recommendation**: [Your suggestion]
```

### 5. Rollback Verification

**Before marking complete, verify rollback is possible:**

// turbo
```bash
# Verify git state allows rollback
git log --oneline -5
git stash list
```

### 6. Completion

// turbo
```bash
npm run build && npm test
```

```markdown
## Execution Complete

### Completed
- [x] Phase 1
- [x] Phase 2

### Key Changes
- Created: [files]
- Modified: [files]

### Rollback Command
git revert [commit-range]

### Next Steps
- Code review
- Deploy to staging
```

---

## Best Practices

- ✅ Complete one batch before next
- ✅ Run checks between phases
- ✅ Keep user informed
- ✅ Verify rollback capability
- ❌ Don't skip ahead
- ❌ Don't exceed plan scope
