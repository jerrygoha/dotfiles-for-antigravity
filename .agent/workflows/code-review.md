---
description: Code review checklist for quality and security
---

# Code Review Workflow (Dev-Master Edition)

Execute a deep, strategic code review focusing on Architecture, Security, and Maintainability.

## When to Use

- **Before Commit**: Mandatory check for all changes.
- **Pull Request**: Pre-flight check before assigning human reviewers.
- **Security Audit**: When touching sensitive logic (Auth, Payments).
- **Refactoring**: Verification of behavior preservation.

---

## 1. Automated Quality Gate

First, ensure the basics are sound. If these fail, **STOP** and request fixes.

// turbo
```bash
# Check for staged changes
git diff --cached --stat > /dev/null || { echo "No staged changes found."; exit 1; }

# Run static analysis & tests (Adjust commands for your project)
echo "Running Quality Checks..."
(npm run lint 2>/dev/null || echo "⚠️ Lint script missing or failed") && \
(npm test 2>/dev/null || echo "⚠️ Test script missing or failed")
```

---

## 2. Semantic Analysis (The Dev-Master Eye)

**Instruction**: Do not just read the code. **Understand the intent.**
Analyze the staged changes (`git diff --cached`) with the following lens:

### 🏛️ Architectural Integrity
- Does this change violate **SOLID** principles?
- Is the **Separation of Concerns** maintained?
- Does it introduce tight coupling between disparate components?

### 🧠 Logic & Edge Cases
- Are **Race Conditions** possible?
- How does it handle `null`, `undefined`, or empty states?
- Is the **Big-O complexity** optimal for the expected data scale?

### 🛡️ Security Deep-Dive (OWASP Context)
- **Injection**: Are inputs sanitized? (SQLi, XSS)
- **Auth**: Are permissions checked at the *server* side?
- **Data Exposure**: Are sensitive fields (PII, secrets) logged or returned?

---

## 3. Interactive Review Process

For each identified issue, classify it by severity:

| Severity | Definition | Action |
|----------|------------|--------|
| 🔴 **CRITICAL** | Security vuln, Crash risk, Build break | **MUST FIX** (Block commit) |
| 🟠 **HIGH** | Logic error, Performance leak, Tech debt | **SHOULD FIX** (Request changes) |
| 🟡 **MEDIUM** | Style, Minor optimization, Naming | **RECOMMEND** (Approve with comments) |

---

## 4. Generate Review Report

Output the review in this format:

```markdown
# 🧐 Dev-Master Code Review

## 🚦 Status: [APPROVE / REQUEST CHANGES]

### 🔴 CRITICAL ISSUES
1. `[File:Line]` **[Issue Name]**: [Description]
   - *Exploit/Risk*: [Why is this dangerous?]
   - *Fix*: [Code snippet]

### 🟠 HIGH PRIORITY
1. `[File:Line]` **[Issue Name]**: [Description]
   - *Impact*: [Performance/Maintainability impact]
   - *Suggestion*: [Code snippet]

### 🟡 OPTIMIZATIONS
- `[File:Line]`: [Suggestion for better style or minor perf]

### 💡 General Feedback
- [Architecture/Design comments]
- [Positive feedback on good patterns used]
```

---

## Best Practices

- ✅ **Review Logic, Not Just Syntax**: Catch logical bombs that linters miss.
- ✅ **Think Like an Attacker**: Try to break the code.
- ✅ **Suggest Solutions**: Don't just complain; provide the fix.
- ❌ **No Nitpicking**: If a linter can catch it, ignore it here (unless critical).

---

## Related Workflows

- `/fix-ci` - If Quality Gate fails.
- `/refactor-clean` - To apply architectural fixes.
- `/security-review` - For dedicated security audits.
