---
description: Execute implementation plan in batches with review checkpoints
---

# Execute Plan Workflow

Execute approved implementation plan phase by phase with verification.

## Prerequisites

- Approved plan exists (use `/write-plan` first)
- User has reviewed and approved the plan

---

## Process

### 1. Load Plan

// turbo
```bash
ls -la .agent/plans/*.md 2>/dev/null || echo "No plans found"
```

### 2. Execute in Batches

For each phase:
1. Complete all steps in the phase
2. Run verification checks
3. Report status
4. Wait for approval before next phase

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

**Status Report:**

```markdown
## Phase [N] Complete ✅

**Done:**
- [Changes made]

**Verified:**
- Build: ✅
- Tests: ✅
- Lint: ✅

**Next:** Phase [N+1] - [Description]
Continue? [Y/N]
```

### 4. Handle Blockers

```markdown
## Blocker Encountered

**Issue**: [Description]
**Impact**: High/Medium/Low

**Options:**
1. [Workaround A] - Pros/Cons
2. [Workaround B] - Pros/Cons
3. Skip and revisit later

**Recommendation**: [Suggested approach]
```

### 5. Rollback Verification

// turbo
```bash
# Verify git state allows rollback
git log --oneline -5
```

### 6. Completion Report

```markdown
## Execution Complete ✅

### Completed Phases
- [x] Phase 1: [Name]
- [x] Phase 2: [Name]

### Key Changes
- Created: [X files]
- Modified: [Y files]
- Deleted: [Z files]

### Rollback Command
git revert [commit-range]

### Next Steps
1. Code review
2. Deploy to staging
```

---

## Best Practices

- ✅ Complete one phase fully before next
- ✅ Run verification between phases
- ✅ Keep user informed of progress
- ✅ Verify rollback is possible
- ❌ Don't skip ahead in phases
- ❌ Don't exceed plan scope

---

## Related Workflows

- `/write-plan` - Create plan first
- `/handoff` - For multi-session execution
- `/code-review` - After execution
