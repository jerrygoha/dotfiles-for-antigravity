---
description: Create well-structured pull requests with proper documentation
---

# Create PR Workflow

Create high-quality PRs that are easy to review.

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

### 3. Create PR Description

```markdown
## Summary
[Brief description of what this PR does]

## Changes
- [Change 1]
- [Change 2]

## Type
- [ ] Bug fix
- [ ] Feature
- [ ] Breaking change
- [ ] Documentation

## Testing
- [ ] Unit tests pass
- [ ] Integration tests pass
- [ ] Manual testing completed

## Screenshots
[If applicable for UI changes]

## Related Issues
Closes #[issue]

## Checklist
- [ ] Code follows style guidelines
- [ ] Self-reviewed
- [ ] Documentation updated
- [ ] No console.log or debug code
```

### 4. Create PR

// turbo
```bash
gh pr create --fill
```

### 5. Post-Creation

```bash
# Add reviewers
gh pr edit --add-reviewer @username

# Add labels
gh pr edit --add-label "enhancement"
```

---

## PR Title Convention

Format: `<type>(<scope>): <description>`

**Types:**
- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation
- `refactor`: Code refactoring
- `test`: Adding tests
- `chore`: Maintenance

**Examples:**
- `feat(auth): add OAuth2 login support`
- `fix(api): handle null response correctly`

---

## Best Practices

- ✅ Small, focused PRs (< 400 lines ideal)
- ✅ One concern per PR
- ✅ Clear, descriptive title
- ✅ Screenshots for UI changes
- ✅ Link related issues
- ❌ Don't mix refactoring with features
- ❌ Don't include unrelated changes

---

## Related Workflows

- `/code-review` - Self-review before PR
- `/testing` - Ensure tests pass
