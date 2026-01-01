---
description: Code review checklist for quality and security
---

# Code Review Workflow

Systematic code review process covering quality, security, and performance.

## Pre-Review Checklist

Before starting the review, verify:

- [ ] Build passes successfully
- [ ] All tests pass
- [ ] No linting errors
- [ ] Branch is up-to-date with main

## Code Quality Review

### 1. Readability
- [ ] Clear, descriptive variable and function names
- [ ] Appropriate comments for complex logic
- [ ] Consistent code style with project standards
- [ ] No dead code or commented-out blocks

### 2. Architecture
- [ ] Follows SOLID principles
- [ ] DRY - no duplicate code
- [ ] KISS - simple solutions preferred
- [ ] Proper separation of concerns

### 3. Error Handling
- [ ] All errors are caught and handled appropriately
- [ ] User-friendly error messages
- [ ] Logging for debugging purposes

## Security Audit

### OWASP Top 10 Check
- [ ] **Injection:** Input validation and parameterized queries
- [ ] **Broken Auth:** Proper authentication flow
- [ ] **Sensitive Data:** No secrets in code, encryption where needed
- [ ] **XXE:** XML parsing is secure
- [ ] **Access Control:** Proper authorization checks
- [ ] **Misconfig:** Secure default configurations
- [ ] **XSS:** Output encoding, CSP headers
- [ ] **Deserialization:** Safe deserialization practices
- [ ] **Components:** Dependencies are up-to-date
- [ ] **Logging:** Security events are logged

## Performance Review

- [ ] No N+1 query problems
- [ ] Appropriate use of caching
- [ ] Efficient algorithms (check Big-O complexity)
- [ ] No memory leaks
- [ ] Lazy loading where appropriate

## Final Steps

1. Provide constructive feedback
2. Approve or request changes
3. Follow up on requested changes
