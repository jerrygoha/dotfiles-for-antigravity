---
description: Create detailed implementation plan with bite-sized tasks
---

# Write Plan Workflow

Create a structured implementation plan before starting development.

## When to Use

- Before starting complex features
- When requirements need clarification
- For tasks estimated over 2 hours
- When multiple components are affected

## Plan Structure

### Template

```markdown
# [Feature/Task Name]

## Problem Statement
[What problem does this solve?]

## Goals
- [ ] Primary goal
- [ ] Secondary goals

## Non-Goals
- What is explicitly out of scope

## Technical Approach

### Architecture Overview
[High-level design]

### Components Affected
| Component | Change Type | Description |
|-----------|-------------|-------------|
| [file/module] | New/Modify/Delete | [What changes] |

## Implementation Steps

### Phase 1: [Name]
- [ ] Step 1.1: [Description] (~Xh)
- [ ] Step 1.2: [Description] (~Xh)

### Phase 2: [Name]
- [ ] Step 2.1: [Description] (~Xh)

## Risks & Mitigations
| Risk | Impact | Mitigation |
|------|--------|------------|
| [Risk] | High/Med/Low | [Strategy] |

## Testing Strategy
- Unit tests for [...]
- Integration tests for [...]
- Manual verification: [...]

## Rollback Plan
[How to revert if something goes wrong]

## Estimated Timeline
- Phase 1: X hours
- Phase 2: X hours
- Total: X hours
```

## Best Practices

1. **Break down tasks** - Each step should be 30min - 2h max
2. **Identify dependencies** - What needs to happen first?
3. **Consider edge cases** - What could go wrong?
4. **Define done** - How do we know it's complete?

## Save Location

// turbo
```bash
mkdir -p .agent/plans
# Save to .agent/plans/YYYY-MM-DD-[feature-name].md
```

## Next Step

After creating the plan:
- Review with user/team
- Use `/execute-plan` to begin implementation
