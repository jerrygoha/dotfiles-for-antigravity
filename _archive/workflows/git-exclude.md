---
description: Add files or patterns to Git exclude (local only, not shared)
---

# Git Exclude Workflow

Add files or patterns to `.git/info/exclude` for local-only git ignores.

## When to Use

Use git exclude when you want to ignore files **locally** without:
- Modifying `.gitignore` (which is committed)
- Affecting other team members

Common use cases:
- Personal IDE settings
- Local test files
- Temporary debugging files
- Machine-specific configurations

## Process

### 1. Check Current Excludes

// turbo
```bash
cat .git/info/exclude 2>/dev/null || echo "No excludes file yet"
```

### 2. Add Pattern

```bash
# Add single file
echo "my-local-file.txt" >> .git/info/exclude

# Add pattern
echo "*.local" >> .git/info/exclude

# Add directory
echo "my-local-dir/" >> .git/info/exclude
```

### 3. Verify Pattern Works

// turbo
```bash
# Check if file is now ignored
git status --ignored
```

## Pattern Syntax

| Pattern | Meaning |
|---------|---------|
| `filename` | Ignore specific file |
| `*.ext` | Ignore all files with extension |
| `dirname/` | Ignore directory |
| `!important.txt` | Negate (don't ignore) |
| `**/temp` | Match in any subdirectory |

## Examples

```bash
# Ignore all .local files
echo "*.local" >> .git/info/exclude

# Ignore personal notes
echo "NOTES.md" >> .git/info/exclude

# Ignore local environment override
echo ".env.local" >> .git/info/exclude

# Ignore personal test directory
echo "my-tests/" >> .git/info/exclude
```

## Difference: exclude vs .gitignore

| Aspect | `.git/info/exclude` | `.gitignore` |
|--------|---------------------|--------------|
| Scope | Local only | Shared with team |
| Committed | No | Yes |
| Use case | Personal preferences | Project requirements |

## Best Practices

- ✅ Use for personal/machine-specific ignores
- ✅ Document why you're excluding something
- ❌ Don't use for project-wide ignores (use .gitignore)
- ❌ Don't exclude files others might need to see
