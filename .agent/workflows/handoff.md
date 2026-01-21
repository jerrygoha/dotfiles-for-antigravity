---
description: Save session context for continuation in new session (100K+ tokens)
---

# Handoff Workflow

Save session context to continue work in a new session.

## When to Use

- Session approaching 100K+ tokens
- Complex debugging in progress
- Milestone completed
- Stopping work temporarily

---

## Process

### 1. Create Handoff Document

Save to: `.agent/handoffs/YYYY-MM-DD-[slug].md`

### 2. Document Structure

```markdown
# [Readable Summary]

## 1. Primary Request and Intent
[Original user request and goal]

## 2. Key Technical Concepts
- [Concept 1]
- [Concept 2]

## 3. Files and Code Sections
### [filename]
- **Why important**: [Reason]
- **Changes made**: [Changes]

## 4. Problem Solving
[Problems solved and ongoing troubleshooting]

## 5. Pending Tasks
- [ ] Task 1
- [ ] Task 2

## 6. Current Work
[Work in progress at handoff time]

## 7. Next Steps
[Recommended next actions]

## 8. Failed Approaches (Important!)
- [Approach that didn't work and why]
```

---

## What to Include

**MUST include:**
- Primary intent and context
- File paths (not full code)
- Pending tasks with clear descriptions
- Failed approaches to avoid repeating

**DON'T include:**
- Full code blocks (use paths instead)
- Obvious information
- Completed/irrelevant context

---

## Best Practices

- ✅ Record key decisions made
- ✅ Include failed approaches (prevent repeating)
- ✅ Use exact file paths
- ✅ List specific pending tasks
- ❌ Don't copy entire code blocks
- ❌ Don't include completed context

---

## Related Workflows

- `/pickup` - Restore session from handoff
- `/learn` - Extract patterns from session
