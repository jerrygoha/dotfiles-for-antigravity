---
description: Restore session context from handoff document
---

# Pickup Workflow

Restore session context from a previous handoff document.

## When to Use

- Starting new session after `/handoff`
- Continuing someone else's work
- Resuming after break

---

## Process

### 1. List Available Handoffs

// turbo
```bash
ls -la .agent/handoffs/*.md 2>/dev/null || echo "No handoffs found"
```

### 2. Read Handoff Document

Specify the handoff file to restore:

```
/pickup [filename]
```

Example: `/pickup 2026-01-21-oauth-implementation`

### 3. Context Restoration

After reading the handoff document:
1. Review **Pending Tasks** first
2. Check **Current Work** section
3. Note **Failed Approaches** to avoid repeating
4. Confirm **Next Steps** are still valid

---

## Verification Steps

After pickup, verify:
- [ ] File paths still exist
- [ ] No conflicting changes made
- [ ] Pending tasks are still relevant
- [ ] Dependencies haven't changed

---

## Best Practices

- ✅ Read entire handoff document
- ✅ Start with Pending Tasks
- ✅ Check for code changes since handoff
- ✅ Review Failed Approaches
- ❌ Don't assume context without reading
- ❌ Don't skip Failed Approaches section

---

## Related Workflows

- `/handoff` - Save session context
- `/learn` - Extract patterns
