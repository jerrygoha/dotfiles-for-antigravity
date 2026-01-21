---
description: TDD-based systematic debugging with evidence-driven root cause analysis
---

# Debug Workflow

Evidence-based debugging using Test-Driven approach. **추론만으로 해결하지 않고, 반드시 실행 결과로 검증한다.**

## Core Principle

> ❌ "이것이 원인인 것 같다" → 수정  
> ✅ "테스트로 재현 → 원인 확인 → 수정 → 테스트 통과" 

---

## Six-Phase Process

### Phase 0: Reproduction Test (MANDATORY)

**수정 전에 실패하는 테스트를 먼저 작성한다.**

```javascript
// Example: Bug reproduction test
describe('BUG-123: User login fails', () => {
  it('should reproduce the reported issue', () => {
    // Arrange: 버그 리포트의 정확한 조건 재현
    const user = { email: 'test@example.com', password: 'valid' };
    
    // Act: 문제 발생 동작 실행
    const result = login(user);
    
    // Assert: 현재 (버그) 동작 확인 - 이 테스트는 FAIL해야 함
    expect(result.success).toBe(true); // 현재 false 반환 → FAIL
  });
});
```

// turbo
```bash
# Run reproduction test - MUST FAIL before fix
npm test -- --testPathPattern="BUG-123"
```

**체크포인트:**
- [ ] 테스트가 버그 조건을 정확히 재현하는가?
- [ ] 테스트가 현재 FAIL하는가?
- [ ] 수정 후 이 테스트가 PASS하면 버그가 해결된 것인가?

---

### Phase 1: Evidence Collection

**추론이 아닌 실행 데이터 수집**

// turbo
```bash
# Collect runtime evidence
node --trace-warnings app.js 2>&1 | tee debug.log

# Check error patterns
grep -E "(Error|Exception|FAIL)" debug.log

# Memory/performance profiling if needed
node --inspect app.js
```

**Evidence Checklist:**
| 증거 유형 | 수집 방법 | 수집 여부 |
|----------|----------|---------|
| Error stack trace | 로그 파일 / 콘솔 | [ ] |
| Input data | 재현 케이스 기록 | [ ] |
| System state | 환경 변수, 설정 | [ ] |
| Timeline | 언제부터 발생? | [ ] |

---

### Phase 2: Hypothesis Formation

**증거 기반 가설 수립 (최소 3개)**

```markdown
## Hypothesis List

| # | 가설 | 근거 (Evidence) | 검증 방법 |
|---|-----|----------------|----------|
| H1 | Race condition in async handler | Stack trace shows Promise rejection | Add delay test |
| H2 | Null reference from API response | Error occurs only with empty response | Mock empty response |
| H3 | Cache stale data | Works after cache clear | Test with/without cache |
```

> ⚠️ **Anti-Pattern**: 증거 없이 "아마 ~일 것이다"로 가설 세우지 않기

---

### Phase 3: Test-Driven Verification

**각 가설을 테스트 코드로 검증**

```javascript
// H1 검증: Race condition test
describe('H1: Race condition hypothesis', () => {
  it('should handle concurrent requests correctly', async () => {
    // 가설이 맞다면 이 테스트가 실패해야 함
    const results = await Promise.all([
      handler(request1),
      handler(request2),
    ]);
    expect(results).toEqual([expected1, expected2]);
  });
});
```

// turbo
```bash
# Run hypothesis tests
npm test -- --testPathPattern="hypothesis"
```

**Verification Matrix:**

| 가설 | 테스트 작성 | 실행 결과 | 결론 |
|-----|-----------|---------|------|
| H1 | `h1.test.js` | FAIL | ✅ 원인 확인 |
| H2 | `h2.test.js` | PASS | ❌ 배제 |
| H3 | `h3.test.js` | PASS | ❌ 배제 |

---

### Phase 4: Fix Implementation

**확인된 원인에 대해서만 수정**

```markdown
## Fix Strategy

**Root Cause**: [Phase 3에서 확인된 원인]
**Evidence**: [테스트 결과 및 로그]

### Changes:
1. [파일명]: [변경 내용]
2. [파일명]: [변경 내용]
```

---

### Phase 5: Verification & Regression

**수정 후 전체 검증**

// turbo
```bash
# 1. Reproduction test must PASS now
npm test -- --testPathPattern="BUG-123"

# 2. All related tests must pass
npm test -- --testPathPattern="related-module"

# 3. Full regression test
npm test
```

**Final Checklist:**
- [ ] Phase 0의 재현 테스트가 PASS하는가?
- [ ] 기존 테스트가 모두 PASS하는가?
- [ ] 새로운 regression이 없는가?

---

### Phase 6: Documentation

```markdown
## Bug Resolution Report

### Issue
[원래 문제 설명]

### Root Cause
[증거와 함께 확인된 원인]

### Evidence
- Test: `[테스트 파일]` - 재현 성공
- Log: `[관련 로그]`
- Verification: 가설 H1 확인됨

### Fix Applied
[구체적인 변경 사항]

### Prevention
[재발 방지를 위한 조치]
- [ ] 관련 테스트 케이스 추가
- [ ] 코드 리뷰 체크리스트 항목 추가
```

---

## Anti-Patterns

| ❌ 하지 말 것 | ✅ 해야 할 것 |
|-------------|-------------|
| 추론만으로 코드 수정 | 테스트로 원인 확인 후 수정 |
| "아마 이게 문제일 것" | "이 테스트가 실패하므로 원인 확인됨" |
| 여러 가설 동시 수정 | 한 번에 하나씩 검증 |
| 수정 후 수동 확인만 | 자동화된 테스트로 검증 |

---

## Quick Reference

```
버그 리포트 → Phase 0 (재현 테스트) → Phase 1 (증거 수집)
    → Phase 2 (가설 3개+) → Phase 3 (테스트 검증)
    → Phase 4 (수정) → Phase 5 (전체 검증) → Phase 6 (문서화)
```
