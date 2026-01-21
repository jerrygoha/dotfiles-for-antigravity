---
description: Web research with citations and evidence-based analysis
---

# Research Workflow

**Multi-source verification required.** 단일 출처 의존 금지.

---

## When to Use

- 새로운 기술/라이브러리 평가
- 아키텍처 결정 시 근거 필요
- 복잡한 버그 트러블슈팅
- 베스트 프랙티스 조사

---

## Process

### 1. Define Research Scope

```markdown
## Research Question
[명확한 질문 형태로 작성]

## Constraints
- Time: [X hours]
- Priority: [High/Med/Low]
- Decision deadline: [Date]

## Success Criteria
- [ ] 최소 3개 독립 출처에서 검증
- [ ] 반대 의견/단점도 조사
- [ ] 실제 사용 사례 포함
```

---

### 2. Multi-Source Verification (MANDATORY)

> ⚠️ **Rule**: 모든 주장은 최소 2개 이상 독립 출처로 검증

**Source Hierarchy:**

| Tier | 출처 유형 | 신뢰도 | 예시 |
|------|---------|-------|-----|
| 1 | Official Docs | ⭐⭐⭐⭐⭐ | MDN, RFC, Language specs |
| 2 | Primary Source | ⭐⭐⭐⭐ | GitHub repo, Author blog |
| 3 | Curated | ⭐⭐⭐ | Awesome lists, Tech blogs |
| 4 | Community | ⭐⭐ | Stack Overflow, Forums |
| 5 | AI/Aggregated | ⭐ | 반드시 상위 Tier로 검증 |

**Verification Template:**

```markdown
## Claim: "[주장 내용]"

| Source | Type | URL | Confirms? |
|--------|------|-----|-----------|
| [Name] | Tier 1 | [URL] | ✅/❌ |
| [Name] | Tier 2 | [URL] | ✅/❌ |

**Verdict**: [Verified / Partially / Unverified]
```

---

### 3. Recency Check

// turbo
```bash
# Check if information is current
echo "Today: $(date +%Y-%m-%d)"
echo "Source date: [YYYY-MM-DD]"
echo "Age: [X months/years]"
```

**Validity Period by Type:**

| 정보 유형 | 유효 기간 |
|----------|----------|
| Library version specific | 해당 버전까지 |
| Security | 6개월 이내 권장 |
| Best practices | 1-2년 |
| Core concepts | Relatively stable |

---

### 4. Analyze & Compare

**Comparison Matrix (for tech decisions):**

```markdown
## [Topic] Comparison

| Criteria | Weight | Option A | Option B | Option C |
|----------|--------|----------|----------|----------|
| Performance | 0.3 | 8 (2.4) | 6 (1.8) | 9 (2.7) |
| Learning Curve | 0.2 | 5 (1.0) | 8 (1.6) | 4 (0.8) |
| Community | 0.2 | 9 (1.8) | 7 (1.4) | 6 (1.2) |
| Maintenance | 0.15 | 7 (1.05) | 8 (1.2) | 5 (0.75) |
| Bundle Size | 0.15 | 6 (0.9) | 5 (0.75) | 8 (1.2) |
| **Total** | 1.0 | **7.15** | **6.75** | **6.65** |

Weights based on: [project requirements/constraints]
```

---

### 5. Document Findings

```markdown
## Research: [Topic]
Date: [YYYY-MM-DD]

### Key Findings

1. **[Finding 1]**
   - Source: [Name](URL) (Tier X)
   - Verified by: [Name](URL) (Tier X)

2. **[Finding 2]**
   - Source: [Name](URL)
   - ⚠️ Single source - requires verification

### Pros & Cons

**Option A**
- ✅ [Pro with source]
- ✅ [Pro with source]
- ❌ [Con with source]

### Counterarguments Considered
- [Alternative viewpoint](URL)

### Recommendation
[Recommendation with evidence-based reasoning]

### Unverified Claims
- [ ] [Claim that needs more sources]
```

---

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
| 단일 출처만 인용 | 최소 2개 독립 출처 검증 |
| "~라고 알려져 있다" | "[출처]에 따르면 ~" |
| 날짜 없는 정보 사용 | 출처 날짜 확인 및 기록 |
| 장점만 나열 | 단점/리스크도 조사 |
| AI 출력 그대로 인용 | Tier 1-3 출처로 검증 |

---

## Citation Format

```markdown
According to [Official Docs](URL) (2024):
> "Direct quote"

This aligns with [GitHub Discussion](URL) where maintainers confirmed...
```
