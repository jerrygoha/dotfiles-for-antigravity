---
description: Create detailed handoff document for session continuity
---

# Handoff Workflow

Create a comprehensive summary to enable seamless continuation of work.

## Goal

Create a detailed summary capturing all technical context, decisions, and next steps so work can be resumed without losing context.

## Process

### 1. Analyze Conversation

Before creating the handoff, analyze:
- User's explicit requests and intents
- Key decisions made
- Technical concepts and patterns used
- Files modified or created

### 2. Create Handoff Document

Structure your handoff as follows:

```markdown
# [Readable Summary]

## 1. Primary Request and Intent
[Detailed description of all user requests and intents]

## 2. Key Technical Concepts
- [Concept 1]
- [Concept 2]

## 3. Files and Code Sections

### [File Name 1]
- **Why important**: [Summary]
- **Changes made**: [Description]
- **Code snippet**:
```language
[Important Code Snippet]
```

## 4. Problem Solving
[Description of solved problems and ongoing troubleshooting]

## 5. Pending Tasks
- [ ] Task 1
- [ ] Task 2

## 6. Current Work
[What was being worked on immediately before handoff]

## 7. Next Steps
[Recommended next actions aligned with user's goals]
```

### 3. Save Handoff

// turbo
Save the handoff document:
```bash
mkdir -p .agent/handoffs
# Save to .agent/handoffs/YYYY-MM-DD-[slug].md
```

### 4. Notify User

Tell the user:
- The handoff file location
- How to resume: `/pickup [filename]`

## Handoff Naming Convention

Create a "slug" for the handoff:

**Examples:**
- `current-user-api-handler`
- `implement-auth`
- `fix-issue-42`
- `refactor-database-layer`

**Full filename:** `2024-01-15-implement-auth.md`
