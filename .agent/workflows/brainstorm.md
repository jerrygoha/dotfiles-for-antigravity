---
description: Interactive design refinement using Socratic method
---

# Brainstorm Workflow

Use this workflow for creative problem-solving and design refinement through structured questioning.

## Process

### Phase 1: Problem Clarification

1. Ask clarifying questions about the problem:
   - What is the core challenge?
   - What constraints exist?
   - What has been tried before?

2. Restate the problem in your own words to confirm understanding.

### Phase 2: Divergent Thinking

1. Generate multiple solution approaches (aim for 3-5 alternatives)
2. For each approach, identify:
   - Pros and cons
   - Required resources
   - Potential risks
   - Time to implement

### Phase 3: Convergent Analysis

1. Compare solutions against constraints
2. Use weighted criteria to evaluate:
   - Feasibility (1-5)
   - Maintainability (1-5)
   - Performance impact (1-5)
   - User experience (1-5)

### Phase 4: Recommendation

1. Present top 2-3 solutions with rationale
2. Ask user for preference or additional constraints
3. Refine based on feedback

## Example Usage

```
User: I need to implement caching for our API

Brainstorm Response:
1. What type of data are we caching? (Read-heavy? Write-heavy?)
2. What's the expected cache hit rate?
3. Do we need distributed caching or local is enough?
...
```

## Output Format

```markdown
## Problem Statement
[Restated problem]

## Solution Options
### Option 1: [Name]
- **Approach**: ...
- **Pros**: ...
- **Cons**: ...
- **Effort**: Low/Medium/High

### Option 2: [Name]
...

## Recommendation
[Recommended approach with reasoning]
```
