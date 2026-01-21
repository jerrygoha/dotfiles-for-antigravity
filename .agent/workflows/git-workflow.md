---
description: Git workflow for branching, commits, and PRs
---

# Git Workflow

Standard git workflow for branching, commits, and pull requests.

---

## Branch Creation

### 1. Start from updated main

```bash
git checkout main && git pull origin main
```

### 2. Create feature branch

```bash
git checkout -b <type>/<short-description>
```

**Branch Types:**
| Type | Use Case |
|------|----------|
| `feat/` | New features |
| `fix/` | Bug fixes |
| `refactor/` | Code refactoring |
| `docs/` | Documentation |
| `test/` | Adding tests |
| `chore/` | Maintenance |

**Examples:**
- `feat/user-authentication`
- `fix/login-redirect`
- `refactor/api-client`

---

## Commit Conventions

**Format:**
```
<type>(<scope>): <description>

[optional body]
[optional footer]
```

**Types:** `feat`, `fix`, `docs`, `style`, `refactor`, `test`, `chore`, `perf`, `ci`

**Examples:**
- `feat(auth): add OAuth2 login support`
- `fix(api): handle null response correctly`
- `docs: update README with setup steps`
- `refactor(db): optimize query performance`

**Rules:**
- Use imperative mood ("add" not "added")
- First line < 72 characters
- Reference issues in footer: `Closes #123`

---

## Commit Best Practices

- ✅ One logical change per commit
- ✅ Tests pass before committing
- ✅ Clear, descriptive messages
- ✅ Small, reviewable commits
- ❌ Don't commit WIP code to shared branches
- ❌ Don't mix unrelated changes

---

## Pull Request Workflow

### 1. Push branch

```bash
git push -u origin <branch-name>
```

### 2. Create PR

```bash
gh pr create --fill
```

### 3. PR Guidelines

- Clear title following commit convention
- Description of changes
- Link to related issues
- Screenshots for UI changes
- Request reviews from appropriate team members

---

## Merge Strategy

| Strategy | When to Use |
|----------|-------------|
| **Squash merge** | Feature branches (clean history) |
| **Rebase merge** | Long-running branches |
| **Merge commit** | Release branches |

**After merge:** Delete the feature branch

---

## Related Workflows

- `/create-pr` - Detailed PR creation
- `/code-review` - Pre-commit review
