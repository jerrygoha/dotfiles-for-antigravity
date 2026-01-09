---
description: Create well-structured pull requests with proper documentation
---

# Create PR Workflow

High-quality PRs that are easy to review.

---

## Prerequisites

- Changes committed to feature branch
- Tests pass locally
- Branch up-to-date with target

---

## Process

### 1. Prepare Branch

// turbo
```bash
git fetch origin && git rebase origin/main
```

### 2. Review Changes

// turbo
```bash
git log origin/main..HEAD --oneline
git diff origin/main --stat
```

### 3. PR Description

```markdown
## Summary
[Brief description]

## Changes
- [Change 1]
- [Change 2]

## Type
- [ ] Bug fix
- [ ] Feature
- [ ] Breaking change
- [ ] Docs

## Testing
- [ ] Unit tests
- [ ] Integration tests
- [ ] Manual testing

## Screenshots
[If applicable]

## Related
Closes #[issue]

## Checklist
- [ ] Style guidelines followed
- [ ] Self-reviewed
- [ ] Docs updated
```

### 4. Create PR

// turbo
```bash
gh pr create
```

### 5. Post-Creation

```bash
gh pr edit --add-reviewer @username
gh pr edit --add-label "enhancement"
```

---

## Best Practices

- ✅ Small, focused PRs
- ✅ One concern per PR
- ✅ Clear title
- ✅ Screenshots for UI
- ❌ Don't mix refactoring with features
