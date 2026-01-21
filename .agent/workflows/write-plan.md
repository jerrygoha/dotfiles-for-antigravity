---
description: Create detailed implementation plan with bite-sized tasks
---

# Write Plan Workflow

Structured planning before development for complex features.

---

## When to Use

- Complex features (2+ hours)
- Multiple components affected
- Requirements need clarification
- Team coordination needed
- High-risk changes

---

## Plan Template

```markdown
# [Feature Name]

## Problem Statement
[What problem does this solve?]

## Goals
- [ ] Primary goal
- [ ] Secondary goals

## Non-Goals (Explicitly out of scope)
- [What we're NOT doing]

## Technical Approach

### Architecture
[High-level design or diagram]

### Components Affected
| Component | Change | Description |
|-----------|--------|-------------|
| [file] | New/Modify/Delete | [What changes] |

## Implementation Steps

### Phase 1: [Name] (~Xh)
- [ ] Step 1.1: [Specific task]
- [ ] Step 1.2: [Specific task]
- [ ] Verification: [How to verify phase complete]

### Phase 2: [Name] (~Xh)
- [ ] Step 2.1: [Specific task]
- [ ] Verification: [How to verify]

## Risk Assessment

| Risk | Probability (1-5) | Impact (1-5) | Score | Mitigation |
|------|-------------------|--------------|-------|------------|
| [Risk] | P | I | P×I | [Strategy] |

> Score >= 15: Requires explicit approval
> Score 10-14: Document mitigation plan
> Score < 10: Accept and proceed

## Testing Strategy
- Unit: [What to test]
- Integration: [What to test]
- Manual: [What to verify]

## Rollback Plan
[How to revert if needed]

## Timeline
- Phase 1: Xh
- Phase 2: Xh
- **Total**: Xh
```

---

## Best Practices

1. **Small steps** - 30min to 2h each
2. **Dependencies first** - Order matters
3. **Quantify risks** - Use P×I scoring
4. **Define done** - Clear completion criteria for each phase
5. **Include verification** - How to know each phase is complete

---

## Save Location

// turbo
```bash
mkdir -p .agent/plans
# Save: .agent/plans/YYYY-MM-DD-[feature].md
```

---

## After Plan Approval

```
→ /execute-plan
```

---

## Related Workflows

- `/brainstorm` - For option selection before planning
- `/research` - For technical investigation before planning
- `/execute-plan` - Execute the approved plan
