---
description: Git workflow for branching, commits, and PRs
---

# Git Workflow

Follow this workflow for managing Git operations.

## Branch Creation

1. Ensure you're on the main branch:
```bash
git checkout main && git pull origin main
```

2. Create a feature branch with descriptive name:
```bash
git checkout -b <type>/<short-description>
```

**Branch Types:**
- `feat/` - New features
- `fix/` - Bug fixes
- `refactor/` - Code refactoring
- `docs/` - Documentation updates
- `test/` - Adding tests

## Commit Conventions

Use semantic commit messages:

```
<type>(<scope>): <description>

[optional body]
[optional footer]
```

**Types:** `feat`, `fix`, `docs`, `style`, `refactor`, `test`, `chore`

**Examples:**
- `feat(auth): add OAuth2 login support`
- `fix(api): handle null response correctly`
- `docs: update README with new setup steps`

## Pull Request Creation

// turbo
1. Push your branch:
```bash
git push origin <branch-name>
```

2. Create PR with:
   - Clear title following commit convention
   - Description of changes
   - Link to related issues
   - Screenshots for UI changes

3. Request review from appropriate team members

## Merge Strategy

- Use **squash merge** for feature branches
- Use **rebase merge** for long-running branches
- Delete branch after merge
