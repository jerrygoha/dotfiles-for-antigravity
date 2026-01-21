---
description: Web research with citations and evidence-based analysis
---

# Research Workflow

Multi-source verification for technical research. **Single source dependency prohibited.**

---

## When to Use

- Evaluating new technology/library
- Architecture decision evidence
- Complex bug troubleshooting
- Best practices investigation

---

## Process

### 1. Define Research Scope

```markdown
## Research Question
[Clear question format]

## Constraints
- Time: [X hours]
- Priority: High/Medium/Low
- Decision deadline: [Date]

## Success Criteria
- [ ] Minimum 3 independent sources verified
- [ ] Counterarguments investigated
- [ ] Real-world usage cases included
```

### 2. Multi-Source Verification (MANDATORY)

> ⚠️ **Rule**: All claims must be verified by 2+ independent sources

**Source Hierarchy:**

| Tier | Source Type | Reliability | Examples |
|------|------------|-------------|----------|
| 1 | Official Docs | ⭐⭐⭐⭐⭐ | MDN, RFC, Language specs |
| 2 | Primary Source | ⭐⭐⭐⭐ | GitHub repo, Author blog |
| 3 | Curated | ⭐⭐⭐ | Awesome lists, Tech blogs |
| 4 | Community | ⭐⭐ | Stack Overflow, Forums |
| 5 | AI/Aggregated | ⭐ | Must verify with Tier 1-3 |

**Verification Template:**

```markdown
## Claim: "[Claim content]"

| Source | Type | URL | Confirms? |
|--------|------|-----|-----------|
| [Name] | Tier 1 | [URL] | ✅/❌ |
| [Name] | Tier 2 | [URL] | ✅/❌ |

**Verdict**: Verified / Partially / Unverified
```

### 3. Recency Check

**Validity Period by Type:**

| Information Type | Valid Period |
|-----------------|--------------|
| Library version specific | Until that version |
| Security | < 6 months recommended |
| Best practices | 1-2 years |
| Core concepts | Generally stable |

### 4. Compare Options

**Comparison Matrix:**

```markdown
| Criteria | Weight | Option A | Option B | Option C |
|----------|--------|----------|----------|----------|
| Performance | 0.3 | 8 (2.4) | 6 (1.8) | 9 (2.7) |
| Learning Curve | 0.2 | 5 (1.0) | 8 (1.6) | 4 (0.8) |
| Community | 0.2 | 9 (1.8) | 7 (1.4) | 6 (1.2) |
| Maintenance | 0.15 | 7 (1.05) | 8 (1.2) | 5 (0.75) |
| Bundle Size | 0.15 | 6 (0.9) | 5 (0.75) | 8 (1.2) |
| **Total** | 1.0 | **7.15** | **6.75** | **6.65** |
```

### 5. Document Findings

```markdown
## Research: [Topic]
Date: YYYY-MM-DD

### Key Findings
1. **[Finding 1]**
   - Source: [Name](URL) (Tier X)
   - Verified by: [Name](URL) (Tier X)

### Pros & Cons
**Option A**
- ✅ [Pro with source]
- ❌ [Con with source]

### Counterarguments Considered
- [Alternative viewpoint](URL)

### Recommendation
[Evidence-based recommendation]

### Unverified Claims
- [ ] [Claim that needs more sources]
```

### 6. Save Research

// turbo
```bash
mkdir -p docs/research
# Save: docs/research/YYYY-MM-DD-[topic].md
```

---

## Anti-Patterns

| ❌ Don't | ✅ Do |
|---------|------|
| Single source citation | Verify with 2+ independent sources |
| "It's known that..." | "According to [source]..." |
| Use undated information | Check and record source date |
| List only pros | Research cons/risks too |
| Quote AI output directly | Verify with Tier 1-3 sources |

---

## Citation Format

```markdown
According to [Official Docs](URL) (2024):
> "Direct quote"

This aligns with [GitHub Discussion](URL) where maintainers confirmed...
```

---

## Related Workflows

- `/brainstorm` - Make decision after research
- `/write-plan` - Plan implementation
