---
description: Resume work from a previous handoff session
---

# Pickup Workflow

Resume work from a previously saved handoff document.

## Process

### 1. List Available Handoffs

If no specific handoff is requested, list all available:

// turbo
```bash
echo "## Available Handoffs"
echo ""
for file in .agent/handoffs/*.md; do
  if [ -f "$file" ]; then
    title=$(grep -m 1 "^# " "$file" | sed 's/^# //')
    basename=$(basename "$file")
    echo "* \`$basename\`: $title"
  fi
done
echo ""
echo "To pickup a handoff, use: /pickup <filename>"
```

### 2. Load Handoff File

When a specific handoff is requested:

1. Locate the file in `.agent/handoffs/`
2. Handle partial matches or typos
3. If multiple matches exist, ask user to clarify

### 3. Resume Context

After reading the handoff:

1. **Summarize current state**
   - What was completed
   - What is pending

2. **Confirm next steps**
   - List the recommended next actions from handoff
   - Ask user if they want to proceed or modify

3. **Begin work**
   - Continue from where the previous session ended

## Example Usage

```
User: /pickup

Agent: ## Available Handoffs

* `2024-01-15-implement-auth.md`: Implement Authentication
* `2024-01-14-fix-api.md`: Fix API Rate Limiting

To pickup a handoff, use: /pickup <filename>

---

User: /pickup implement-auth

Agent: Resuming "Implement Authentication" handoff...

## Context Restored
- Completed: Basic JWT implementation
- Pending: Refresh token logic, logout endpoint

## Recommended Next Step
Implement refresh token rotation

Shall I continue with this approach?
```

## Notes

- Handoffs are stored in `.agent/handoffs/`
- Each handoff includes full context for seamless continuation
- Use `/handoff` to create new handoff documents
