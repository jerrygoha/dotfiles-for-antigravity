---
description: Create new workflow files following best practices
---

# Create Workflow

Create a new workflow file for `.agent/workflows/` directory.

## Workflow File Structure

### 1. YAML Frontmatter (Required)

```yaml
---
description: Short description visible in workflow list
---
```

### 2. Title and Purpose

```markdown
# [Workflow Name] Workflow

[Brief explanation of when and why to use this workflow]
```

### 3. Process Steps

Numbered phases with:
- Clear step descriptions
- Code examples where applicable
- `// turbo` annotations for auto-run safe commands

### 4. Best Practices

Do's and don'ts for the workflow.

---

## Template

```markdown
---
description: [One-line description]
---

# [Workflow Name] Workflow

[When to use this workflow]

## Prerequisites

- [Prerequisite 1]
- [Prerequisite 2]

## Process

### Phase 1: [Name]

1. [Step 1]
2. [Step 2]

// turbo
\`\`\`bash
[Safe command to run]
\`\`\`

### Phase 2: [Name]

1. [Step 1]
2. [Step 2]

## Output

[What the workflow produces]

## Best Practices

- ✅ Do this
- ✅ Also do this
- ❌ Don't do this

## Related Workflows

- `/workflow-name` - Brief description
```

---

## File Locations

**Project-specific:**
```
.agent/workflows/[workflow-name].md
```

**Shared (dotfiles):**
```
dotfiles-for-antigravity/.agent/workflows/
```

---

## Naming Conventions

- Use kebab-case: `create-pr.md`, `code-review.md`
- Be descriptive but concise
- Use action verbs: `create-`, `fix-`, `run-`, `debug-`

---

## The `// turbo` Annotation

Add `// turbo` above command blocks that are:
- ✅ Read-only operations (ls, cat, grep)
- ✅ Safe to auto-execute (npm test, npm run build)
- ✅ No destructive side effects

**Never use `// turbo` for:**
- ❌ Destructive operations (rm, drop)
- ❌ System modifications (install)
- ❌ External requests with side effects

---

## Testing Your Workflow

1. Save to `.agent/workflows/`
2. Invoke with `/workflow-name`
3. Verify behavior
4. Iterate and refine

---

## Best Practices

- ✅ Single purpose per workflow
- ✅ Clear success criteria
- ✅ Include related workflows
- ✅ Add practical examples
- ❌ Don't make workflows too long
- ❌ Don't duplicate existing workflows
