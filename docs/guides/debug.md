# /debug 완벽 상세 가이드

> TDD 기반 체계적 디버깅으로 근본 원인을 찾는 워크플로우

---

## 📌 개요 및 목적

`/debug`는 **추론이 아닌 증거 기반**으로 버그의 근본 원인을 찾고 해결하는 워크플로우입니다.

**핵심 원칙:**
> ❌ "이것이 원인인 것 같다" → 수정  
> ✅ "테스트로 재현 → 원인 확인 → 수정 → 테스트 통과"

---

## 🎯 언제 사용하나요?

### ✅ 이럴 때 사용하세요

| 상황 | 예시 |
|------|------|
| 버그 발생 | "로그인할 때 에러가 나요" |
| 원인 불명확 | "가끔 데이터가 안 나와요" |
| 여러 가능성 | "여러 곳이 의심되는데..." |
| 재현이 어려움 | "결제할 때 간헐적으로 실패" |
| 복잡한 로직 오류 | "계산 결과가 이상해요" |

### 📋 구체적인 사용 시나리오

```
"사용자가 로그인하면 가끔 세션이 없다고 나와요"

→ /debug 사용
→ Phase 0: 재현 테스트 작성 (FAIL 확인)
→ Phase 1-2: 증거 수집 및 가설 3개
→ Phase 3: 테스트로 가설 검증
→ Phase 4: 수정
→ Phase 5: 전체 테스트 통과 확인
```

---

## 📤 기대 결과물

### 6-Phase 디버깅 프로세스 완료 후

```markdown
## Bug Resolution Report

### Issue
로그인 후 간헐적으로 세션이 없다고 표시됨

### Root Cause
Race condition: 세션 저장 전에 리다이렉트 발생

### Evidence
- Test: `session.test.ts` - 동시 요청 시 실패 재현
- Log: `Promise rejection at auth.ts:45`
- Verification: H1 가설 확인됨

### Fix Applied
- `auth.ts`: await 누락 수정
- 세션 저장 완료 후 리다이렉트

### Prevention
- [x] 재현 테스트 추가됨
- [x] async/await 린트 규칙 추가
```

---

## 📖 상세 사용법 (6-Phase)

### Phase 0: 재현 테스트 (MANDATORY)

**수정 전에 실패하는 테스트를 먼저 작성합니다.**

```javascript
describe('BUG-123: 세션 누락', () => {
  it('should maintain session after login', async () => {
    const result = await login(user);
    expect(result.session).toBeDefined(); // 현재 FAIL해야 함
  });
});
```

**체크포인트:**
- [ ] 테스트가 버그 조건을 재현하는가?
- [ ] 테스트가 현재 FAIL하는가?
- [ ] 수정 후 PASS하면 버그 해결인가?

### Phase 1: 증거 수집

**추론이 아닌 실행 데이터 수집**

```bash
# 런타임 증거 수집
node --trace-warnings app.js 2>&1 | tee debug.log

# 에러 패턴 확인
grep -E "(Error|Exception|FAIL)" debug.log
```

### Phase 2: 가설 형성 (최소 3개)

| # | 가설 | 근거 | 검증 방법 |
|---|-----|------|----------|
| H1 | Race condition | Stack trace에 Promise rejection | 딜레이 테스트 |
| H2 | Null response | 빈 응답 시에만 발생 | 빈 응답 Mock |
| H3 | Cache 문제 | 캐시 클리어 후 정상 | 캐시 유무 테스트 |

### Phase 3: 테스트로 가설 검증

```javascript
// H1 검증
describe('H1: Race condition', () => {
  it('should handle concurrent requests', async () => {
    const results = await Promise.all([
      handler(req1), handler(req2)
    ]);
    expect(results).toEqual([expected1, expected2]);
  });
});
```

### Phase 4: 수정

확인된 원인에 대해서**만** 수정

### Phase 5: 검증 & Regression

```bash
# 재현 테스트 PASS 확인
npm test -- --testPathPattern="BUG-123"

# 전체 regression 테스트
npm test
```

### Phase 6: 문서화

버그 리포트 작성 (위 결과물 참조)

---

## ⚠️ 이런 상황엔 다른 워크플로우를!

| 상황 | 대신 사용할 워크플로우 |
|------|----------------------|
| 빌드 자체가 안 됨 | `/fix-ci` |
| 새 기능 개발 중 테스트 실패 | `/tdd` |
| 원인이 명확함 | 바로 수정 |
| 성능 문제 | `/research` + 프로파일링 |

### 혼동하기 쉬운 상황

**Q: `/debug` vs `/tdd`?**
- `/debug`: 기존 코드의 버그 수정
- `/tdd`: 새 기능 개발 (테스트 먼저)

**Q: 빌드 에러도 `/debug`?**
- 빌드 에러: `/fix-ci`
- 런타임 버그: `/debug`

---

## 🔗 함께 사용하면 좋은 워크플로우

### 버그 수정 흐름

```
/debug               # 버그 해결
    ↓
/testing             # 추가 테스트
    ↓
/code-review         # 수정 검토
    ↓
/learn               # 패턴 기록
```

---

## ✅ 체크리스트

### 디버깅 전

- [ ] 버그 재현 조건 파악했는가?
- [ ] 에러 로그/스택 트레이스 확인했는가?

### 디버깅 중

- [ ] Phase 0 테스트가 FAIL하는가?
- [ ] 최소 3개 가설을 세웠는가?
- [ ] 테스트로 가설을 검증했는가?

### 디버깅 후

- [ ] Phase 0 테스트가 PASS하는가?
- [ ] 전체 테스트가 통과하는가?
- [ ] 문서화 완료했는가?

---

## 💡 안티패턴

| ❌ 하지 말 것 | ✅ 해야 할 것 |
|-------------|-------------|
| 추론만으로 코드 수정 | 테스트로 원인 확인 후 수정 |
| "아마 이게 문제일 것" | "이 테스트가 실패하므로 원인 확인" |
| 여러 가설 동시 수정 | 한 번에 하나씩 검증 |
| 수정 후 수동 확인만 | 자동화 테스트로 검증 |
