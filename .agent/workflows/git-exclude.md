---
description: Add files or patterns to Git exclude (local only, not shared)
---

# Git Exclude Workflow

Add files/patterns to `.git/info/exclude` for local-only git ignores.

## When to Use

Ignore files **locally** without:
- Modifying `.gitignore` (which is committed)
- Affecting other team members

**Common Use Cases:**
- Personal IDE settings
- Local test files
- Temporary debug files
- Machine-specific configs

---

## git exclude vs .gitignore

| Aspect | `.git/info/exclude` | `.gitignore` |
|--------|---------------------|--------------|
| Scope | Local only | Shared with team |
| Committed | No | Yes |
| Use case | Personal preferences | Project requirements |

---

## Process

### 1. Check Current Excludes

// turbo
```bash
cat .git/info/exclude 2>/dev/null || echo "No excludes file"
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
git status --ignored | head -20
```

---

## Pattern Syntax

| Pattern | Meaning |
|---------|---------|
| `filename` | Ignore specific file |
| `*.ext` | Ignore all files with extension |
| `dirname/` | Ignore directory |
| `!important.txt` | Negate (don't ignore) |
| `**/temp` | Match in any subdirectory |

---

## Examples

```bash
# Personal IDE settings
echo ".idea/" >> .git/info/exclude
echo ".vscode/settings.json" >> .git/info/exclude

# Local notes
echo "NOTES.md" >> .git/info/exclude
echo "TODO.local.md" >> .git/info/exclude

# Local environment override
echo ".env.local.backup" >> .git/info/exclude

# Debug files
echo "debug-*.log" >> .git/info/exclude
```

---

## Best Practices

- ✅ Use for personal/machine-specific ignores
- ✅ Document why you're excluding (comment above pattern)
- ❌ Don't use for project-wide ignores (use `.gitignore`)
- ❌ Don't exclude files others might need to track

---

## Related Workflows

- `/git-workflow` - General git operations
