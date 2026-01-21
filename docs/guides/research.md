# /research 완벽 상세 가이드

> 다중 출처 검증 기반의 기술 조사 워크플로우

---

## 📌 개요 및 목적

`/research`는 **여러 출처를 검증**하여 신뢰할 수 있는 정보를 수집하는 워크플로우입니다.

**핵심 원칙:**
> 단일 출처 의존 금지. 모든 주장은 최소 2개 이상 독립 출처로 검증.

---

## 🎯 언제 사용하나요?

### ✅ 이럴 때 사용하세요

| 상황 | 예시 |
|------|------|
| 새 기술 평가 | "Next.js 15 새 기능 조사" |
| 라이브러리 선택 | "상태관리 라이브러리 비교" |
| 아키텍처 결정 근거 | "서버리스 vs 컨테이너" |
| 복잡한 버그 조사 | "이 에러 해결법 찾아줘" |
| 베스트 프랙티스 | "보안 인증 패턴" |

---

## 📤 기대 결과물

### 조사 결과 문서

```markdown
## Research: [Topic]
Date: 2026-01-21

### Key Findings

1. **[Finding 1]**
   - Source: [Official Docs](URL) (Tier 1)
   - Verified by: [GitHub Repo](URL) (Tier 2)

2. **[Finding 2]**
   - Source: [Tech Blog](URL) (Tier 3)
   - ⚠️ Single source - requires verification

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

---

## 📖 상세 사용법

### Step 1: 조사 범위 정의

```
/research Next.js 15의 Server Actions 성능과 보안 이슈 조사해줘.
우리 프로젝트에 적용해도 될지 판단하고 싶어.
```

### Step 2: 출처 계층 이해

| Tier | 출처 유형 | 신뢰도 | 예시 |
|------|---------|-------|-----|
| 1 | Official Docs | ⭐⭐⭐⭐⭐ | MDN, RFC, 공식 문서 |
| 2 | Primary Source | ⭐⭐⭐⭐ | GitHub repo, 저자 블로그 |
| 3 | Curated | ⭐⭐⭐ | Awesome lists, 기술 블로그 |
| 4 | Community | ⭐⭐ | Stack Overflow, 포럼 |
| 5 | AI/Aggregated | ⭐ | 반드시 상위 Tier로 검증 |

### Step 3: 검증 확인

각 주장에 대해 다중 출처 확인:
```markdown
## Claim: "Server Actions는 SQL Injection에 안전하다"

| Source | Type | URL | Confirms? |
|--------|------|-----|-----------|
| Next.js Docs | Tier 1 | [URL] | ✅ |
| Security Blog | Tier 3 | [URL] | ⚠️ 조건부 |

**Verdict**: Partially Verified (입력 검증 필요)
```

### Step 4: 결과물 저장

```bash
docs/research/YYYY-MM-DD-[topic].md
```

---

## ⚠️ 이런 상황엔 다른 워크플로우를!

| 상황 | 대신 사용할 워크플로우 |
|------|----------------------|
| 옵션 비교/결정 | `/brainstorm` |
| 구현 계획 | `/write-plan` |
| 버그 디버깅 | `/debug` |

### 혼동하기 쉬운 상황

**Q: `/research` vs `/brainstorm`?**
- `/research`: 정보 수집 및 검증
- `/brainstorm`: 수집된 정보로 결정

---

## 🔗 함께 사용하면 좋은 워크플로우

```
/research            # 정보 수집
    ↓
/brainstorm          # 옵션 결정
    ↓
/write-plan          # 구현 계획
```

---

## ✅ 조사 품질 체크리스트

### 조사 전

- [ ] 질문이 명확한가?
- [ ] 성공 기준이 있는가?

### 조사 중

- [ ] 최소 2개 독립 출처로 검증했는가?
- [ ] 출처 날짜를 확인했는가?
- [ ] 반대 의견도 조사했는가?

### 조사 후

- [ ] 모든 주장에 출처가 있는가?
- [ ] 미검증 주장이 표시되었는가?
- [ ] 결론이 증거에 기반하는가?

---

## 💡 안티패턴

| ❌ Don't | ✅ Do |
|---------|------|
| 단일 출처만 인용 | 최소 2개 독립 출처 |
| "~라고 알려져 있다" | "[출처]에 따르면 ~" |
| 날짜 없는 정보 | 출처 날짜 기록 |
| 장점만 나열 | 단점/리스크도 조사 |
| AI 출력 그대로 | Tier 1-3으로 검증 |
