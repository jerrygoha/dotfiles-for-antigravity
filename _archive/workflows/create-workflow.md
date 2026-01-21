---
description: Create new workflow files following best practices
---

# Create Workflow

Create a new workflow file for the `.agent/workflows/` directory.

## Workflow File Structure

Every workflow must include:

### 1. YAML Frontmatter

```yaml
---
description: Short description visible in workflow list
---
```

### 2. Clear Title

```markdown
# [Workflow Name]
```

### 3. Purpose Section

When and why to use this workflow.

### 4. Process Steps

Step-by-step instructions with:
- Numbered phases
- Code examples where applicable
- `// turbo` annotations for auto-run safe commands

### 5. Best Practices

Do's and don'ts for the workflow.

## Template

```markdown
---
description: [One-line description]
---

# [Workflow Name] Workflow

[Brief explanation of when to use this workflow]

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
```

## File Locations

**Project-specific workflows:**
```
.agent/workflows/[workflow-name].md
```

**Shared workflows (for dotfiles):**
```
dotfiles-for-antigravity/.agent/workflows/[workflow-name].md
```

## Naming Conventions

- Use kebab-case: `create-pr.md`, `code-review.md`
- Be descriptive but concise
- Use verbs: `create-`, `fix-`, `run-`, `debug-`

## The `// turbo` Annotation

Add `// turbo` above command blocks that are:
- ✅ Read-only operations
- ✅ Safe to auto-execute
- ✅ No side effects
- ❌ NOT destructive operations
- ❌ NOT commands that modify system state

## Testing Your Workflow

1. Copy to your project's `.agent/workflows/`
2. Invoke with `/workflow-name`
3. Verify it behaves as expected
4. Iterate and refine
