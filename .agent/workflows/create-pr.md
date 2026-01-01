---
description: Create well-structured pull requests with proper documentation
---

# Create PR Workflow

Create high-quality pull requests that are easy to review.

## Prerequisites

- Changes are committed to a feature branch
- Tests pass locally
- Branch is up to date with target branch

## Process

### 1. Prepare the Branch

// turbo
```bash
# Ensure you're on your feature branch
git branch --show-current

# Fetch latest and rebase if needed
git fetch origin
git rebase origin/main
```

### 2. Review Your Changes

// turbo
```bash
# Review what will be in the PR
git log origin/main..HEAD --oneline
git diff origin/main --stat
```

### 3. Write PR Description

Follow this template:

```markdown
## Summary
[Brief description of what this PR does]

## Changes
- [Change 1]
- [Change 2]

## Type of Change
- [ ] Bug fix (non-breaking change that fixes an issue)
- [ ] New feature (non-breaking change that adds functionality)
- [ ] Breaking change (fix or feature that would cause existing functionality to not work as expected)
- [ ] Documentation update

## Testing
- [ ] Unit tests added/updated
- [ ] Integration tests added/updated
- [ ] Manual testing performed

## Screenshots
[If applicable, add screenshots here]

## Related Issues
Closes #[issue number]

## Checklist
- [ ] Code follows project style guidelines
- [ ] Self-review completed
- [ ] Comments added for complex logic
- [ ] Documentation updated
```

### 4. Create the PR

// turbo
```bash
# Using GitHub CLI
gh pr create --title "feat: [description]" \
  --body-file PR_TEMPLATE.md \
  --base main

# Or with interactive mode
gh pr create
```

### 5. Post-Creation

1. **Add reviewers**
   ```bash
   gh pr edit --add-reviewer @username
   ```

2. **Add labels**
   ```bash
   gh pr edit --add-label "enhancement"
   ```

3. **Link issues**
   - Reference in description: `Closes #123`

## Best Practices

- ✅ Keep PRs small and focused
- ✅ One concern per PR
- ✅ Clear, descriptive title
- ✅ Screenshots for UI changes
- ❌ Don't mix refactoring with features
- ❌ Don't include unrelated changes
