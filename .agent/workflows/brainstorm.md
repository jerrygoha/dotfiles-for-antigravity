---
description: Interactive design refinement using Socratic method
---

# Brainstorm Workflow

Explore multiple approaches and select optimal solution through structured comparison.

## When to Use

- Technology choice (Library A vs B)
- Architecture decision (Monolith vs Microservices)
- Multiple implementation approaches
- Trade-off analysis needed

---

## Process

### Phase 1: Clarify the Problem

Ask clarifying questions:
- What is the core challenge?
- What are the constraints?
- What was tried before?

Restate problem to confirm understanding.

### Phase 2: Diverge (Generate Options)

Generate 3-5 alternatives. For each option, evaluate:
- Pros/Cons
- Resources needed
- Risks
- Time estimate

### Phase 3: Converge (Evaluate)

**Weighted Evaluation Matrix:**

| Criteria | Weight | Opt A | Opt B | Opt C |
|----------|--------|-------|-------|-------|
| Feasibility | 0.3 | 1-5 | 1-5 | 1-5 |
| Maintainability | 0.25 | 1-5 | 1-5 | 1-5 |
| Performance | 0.25 | 1-5 | 1-5 | 1-5 |
| Developer UX | 0.2 | 1-5 | 1-5 | 1-5 |
| **Weighted Score** | 1.0 | Σ | Σ | Σ |

### Phase 4: Recommend

Present top 2-3 options with rationale, refine based on feedback.

---

## Output Format

```markdown
## Problem
[Restated problem]

## Options

### Option 1: [Name]
- **Approach**: Description
- **Pros**: Benefits
- **Cons**: Drawbacks
- **Effort**: Low/Medium/High
- **Weighted Score**: X.X

### Option 2: [Name]
...

## Recommendation
[Chosen option with reasoning]

## Decision Recorded
Consider creating ADR (Architecture Decision Record)
```

---

## Best Practices

- ✅ Minimum 3 options (avoid false dichotomy)
- ✅ Customize weights for project priorities
- ✅ Consider counterarguments
- ✅ Document decision for future reference
- ❌ Don't rush to first solution
- ❌ Don't ignore cons of preferred option

---

## Related Workflows

- `/research` - Gather information before brainstorming
- `/write-plan` - Plan after decision is made
