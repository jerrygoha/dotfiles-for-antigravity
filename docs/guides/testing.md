# /testing 완벽 상세 가이드

> 고급 테스팅 기법으로 코드 품질을 높이는 워크플로우

---

## 📌 개요 및 목적

`/testing`은 **다양한 테스팅 기법**을 적용하여 테스트 품질을 높이는 워크플로우입니다.

**다루는 기법:**
- Unit Testing (AAA 패턴)
- Edge Case Testing
- Property-Based Testing
- Integration Testing
- Mutation Testing Awareness

---

## 🎯 언제 사용하나요?

### ✅ 이럴 때 사용하세요

| 상황 | 예시 |
|------|------|
| 테스트 품질 향상 | "더 견고한 테스트 필요" |
| Edge case 커버 | "경계값 테스트 추가" |
| Property-based 테스트 | "모든 입력에 대해 검증" |
| Integration 테스트 | "API 통합 테스트" |

### TDD와의 차이

| `/tdd` | `/testing` |
|--------|-----------|
| RED-GREEN-REFACTOR 사이클 | 다양한 테스팅 기법 |
| 새 기능 개발 | 테스트 품질 향상 |
| 기본 테스트 | 고급 테스트 |

---

## 📤 기대 결과물

### 테스트 구조

```
tests/
├── unit/           # 빠른 격리 테스트 (<100ms)
├── integration/    # 외부 의존성 테스트
├── e2e/            # 전체 사용자 플로우
└── fixtures/       # 테스트 데이터
```

### Edge Case 테스트

```typescript
describe('Edge Cases', () => {
  it.each([
    [[], 0],           // 빈 배열
    [[1], 1],          // 단일 요소
    [[-1, -2], -3],    // 음수
    [[0, 0, 0], 0],    // 모두 0
  ])('sum(%p) should be %i', (input, expected) => {
    expect(sum(input)).toBe(expected);
  });
});
```

### Property-Based 테스트

```typescript
import fc from 'fast-check';

describe('Property-based', () => {
  it('sort preserves length', () => {
    fc.assert(fc.property(
      fc.array(fc.integer()),
      (arr) => sort(arr).length === arr.length
    ));
  });
});
```

---

## 📖 상세 사용법

### Step 1: 호출

```
/testing calculateDiscount 함수에 대한 고급 테스트 작성해줘
```

### Step 2: 테스트 유형 선택

에이전트가 제안하는 테스트 유형 확인:
- Edge case
- Property-based
- Integration
- 등

### Step 3: 테스트 작성

### Step 4: 커버리지 확인

```bash
npm test -- --coverage
```

---

## ⚠️ 이런 상황엔 다른 워크플로우를!

| 상황 | 대신 사용할 워크플로우 |
|------|----------------------|
| 새 기능 TDD | `/tdd` |
| E2E 테스트 | `/e2e` |
| 커버리지 분석 | `/test-coverage` |
| 버그 재현 | `/debug` |

---

## 🔗 함께 사용하면 좋은 워크플로우

```
/tdd                 # 기본 테스트 작성
    ↓
/testing             # 고급 테스트 추가
    ↓
/test-coverage       # 커버리지 확인
```

---

## ✅ 커버리지 기준

| 모듈 유형 | Line | Branch |
|----------|------|--------|
| Core/Critical | 90%+ | 85%+ |
| Business Logic | 80%+ | 75%+ |
| Utilities | 100% | 100% |
| UI Components | 70%+ | 60%+ |

---

## 💡 Edge Case 체크리스트

| 입력 유형 | 테스트 케이스 |
|----------|--------------|
| Numbers | 0, -1, MAX_INT, NaN, Infinity |
| Strings | "", " ", 매우 긴 문자열, unicode, null |
| Arrays | [], 단일 요소, 최대 크기 |
| Objects | {}, null, undefined, 중첩 |
