---
description: Remove dead code safely with test verification
---

# Refactor Clean Workflow

Identify and safely remove dead/unused code with test verification.

## When to Use

- Cleaning up technical debt
- Removing deprecated code after migration
- Eliminating unused dependencies
- Post-refactoring cleanup

---

## Process

### 1. Analyze Dead Code

// turbo
```bash
# Find unused exports (TypeScript)
npx ts-prune 2>/dev/null || echo "Install: npm i -g ts-prune"

# Find unused dependencies
npx depcheck 2>/dev/null || echo "Install: npm i -g depcheck"
```

### 2. Categorize Findings

| Level | Description | Action |
|-------|-------------|--------|
| 🟢 SAFE | No references, safe to delete | Auto-remove |
| 🟡 CAUTION | Possible dynamic import | Manual review |
| 🔴 DANGER | Config/entry files | Do not remove |

### 3. Create Removal Report

```markdown
## Dead Code Analysis

### Files to Remove (SAFE)
- `src/utils/deprecated.ts` - No imports
- `src/components/OldButton.tsx` - Not used

### Needs Review (CAUTION)
- `src/api/legacy.ts` - Check for dynamic imports

### Protected (DANGER)
- `src/config/*` - Configuration files
- `src/index.ts` - Entry point
```

### 4. Safe Removal Process

1. Ensure all tests pass BEFORE removal
2. Remove SAFE items only
3. Run tests after each removal
4. Rollback if any test fails

// turbo
```bash
npm test
```

### 5. Cleanup Dependencies

```bash
# Remove unused packages
npm uninstall [package-name]

# Verify no breaking changes
npm run build && npm test
```

---

## Best Practices

- ✅ Always run tests before AND after
- ✅ Remove in small batches
- ✅ Keep separate commits for cleanup
- ✅ Check for dynamic imports (`import()`, `require()`)
- ❌ Don't remove CAUTION/DANGER without review
- ❌ Don't mix cleanup with feature changes

---

## Related Workflows

- `/test-coverage` - Ensure coverage before cleanup
- `/code-review` - Review changes
