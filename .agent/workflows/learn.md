---
description: Extract reusable patterns from current session
---

# Learn Workflow

Extract and save reusable patterns from problems solved in current session.

## When to Use

- After solving complex bug
- Discovered useful pattern
- Found library quirk/workaround
- Created reusable solution

**Don't use for:**
- Simple typo fixes
- Generic coding patterns (well-documented)
- One-time solutions

---

## Process

### 1. Identify Pattern Worth Saving

Ask yourself:
- Will this help in future projects?
- Was this hard to figure out?
- Is this not well-documented elsewhere?

### 2. Create Learning Document

Save to: `.agent/learnings/[pattern-name].md`

```markdown
# [Pattern Name]

**Extracted:** YYYY-MM-DD
**Context:** [When this pattern applies]

## Problem
[What problem does this solve?]

## Solution
\`\`\`typescript
// Code example
\`\`\`

## When to Use
- [Condition 1]
- [Condition 2]

## Common Mistakes
- [Mistake to avoid]

## Related Files
- [File paths where pattern was applied]

## Tags
#tag1 #tag2
```

### 3. Example Pattern

```markdown
# Next.js Hydration Mismatch Fix

**Extracted:** 2026-01-21
**Context:** SSR/CSR mismatch issues

## Problem
Accessing browser APIs during SSR causes hydration errors.

## Solution
\`\`\`typescript
const [mounted, setMounted] = useState(false)

useEffect(() => {
  setMounted(true)
}, [])

if (!mounted) return <Skeleton />
\`\`\`

## When to Use
- Accessing `window` or `document`
- Using `localStorage`
- Browser-only APIs

## Tags
#nextjs #hydration #ssr
```

---

## Best Practices

- ✅ Extract immediately after solving
- ✅ Make patterns reusable (not project-specific)
- ✅ Include working code examples
- ✅ Add tags for searchability
- ❌ Don't save trivial fixes
- ❌ Don't include project-specific details

---

## Related Workflows

- `/handoff` - Save session context (different purpose)
- `/debug` - Often leads to learnings
