# /tdd 완벽 상세 가이드

> 테스트 주도 개발로 안정적인 코드를 작성하는 워크플로우

---

## 📌 개요 및 목적

`/tdd`는 **테스트를 먼저 작성**하고, 테스트를 통과하는 최소한의 코드를 구현하는 워크플로우입니다.

**TDD 사이클:**
```
RED → GREEN → REFACTOR → REPEAT
  ↓      ↓        ↓
실패   통과    개선
```

---

## 🎯 언제 사용하나요?

### ✅ 이럴 때 사용하세요

| 상황 | 예시 |
|------|------|
| 새 함수/유틸리티 | "날짜 포맷팅 함수 만들어줘" |
| 비즈니스 로직 | "할인 계산 로직 구현" |
| 핵심 기능 | "결제 처리 로직" |
| 복잡한 알고리즘 | "정렬 알고리즘 구현" |
| 리팩토링 | "안전하게 리팩토링" |

### 📋 구체적인 사용 시나리오

```
"주문 금액에 따른 할인율 계산 함수를 만들어줘.
10만원 이상 10%, 50만원 이상 15%, 100만원 이상 20%."

→ /tdd 사용
→ Step 1: 인터페이스 정의
→ Step 2: 실패하는 테스트 작성 (RED)
→ Step 3: 최소 구현 (GREEN)
→ Step 4: 리팩토링 (REFACTOR)
→ Step 5: 80%+ 커버리지 확인
```

---

## 📤 기대 결과물

### Step 1: 인터페이스

```typescript
interface CalculateDiscountInput {
  orderAmount: number;
}

interface DiscountResult {
  rate: number;      // 0.1 = 10%
  discountAmount: number;
  finalAmount: number;
}

function calculateDiscount(input: CalculateDiscountInput): DiscountResult;
```

### Step 2: 테스트 (RED)

```typescript
describe('calculateDiscount', () => {
  it('should return 10% for 100,000+', () => {
    const result = calculateDiscount({ orderAmount: 100000 });
    expect(result.rate).toBe(0.1);
    expect(result.discountAmount).toBe(10000);
    expect(result.finalAmount).toBe(90000);
  });

  it('should return 0% for under 100,000', () => {
    const result = calculateDiscount({ orderAmount: 50000 });
    expect(result.rate).toBe(0);
  });
});
```

### Step 3: 구현 (GREEN)

```typescript
function calculateDiscount(input: CalculateDiscountInput): DiscountResult {
  const { orderAmount } = input;
  let rate = 0;

  if (orderAmount >= 1000000) rate = 0.2;
  else if (orderAmount >= 500000) rate = 0.15;
  else if (orderAmount >= 100000) rate = 0.1;

  const discountAmount = orderAmount * rate;
  const finalAmount = orderAmount - discountAmount;

  return { rate, discountAmount, finalAmount };
}
```

### Step 4: 커버리지

```
PASS tests/discount.test.ts
  ✓ should return 10% for 100,000+ (2ms)
  ✓ should return 15% for 500,000+ (1ms)
  ✓ should return 20% for 1,000,000+ (1ms)
  ✓ should return 0% for under 100,000 (1ms)

Coverage: 100%
```

---

## 📖 상세 사용법

### Step 1: 워크플로우 호출

```
/tdd 할인율 계산 함수 만들어줘.
- 10만원 이상: 10%
- 50만원 이상: 15%
- 100만원 이상: 20%
- 소수점은 버림
```

### Step 2: 인터페이스 확인

에이전트가 인터페이스를 제안합니다. 확인 후:
```
"좋아, 진행해"
또는
"반환값에 세금 정보도 추가해줘"
```

### Step 3: RED 단계 확인

에이전트가 테스트를 작성하고 **실패를 확인**합니다.
```bash
FAIL tests/discount.test.ts
  ✕ should return 10% for 100,000+
```

### Step 4: GREEN 단계

테스트를 통과하는 **최소한의** 코드 구현

### Step 5: REFACTOR 단계

코드 품질 개선 (테스트는 계속 통과해야 함)

### Step 6: 커버리지 확인

```bash
npm test -- --coverage
```

---

## ⚠️ 이런 상황엔 다른 워크플로우를!

| 상황 | 대신 사용할 워크플로우 |
|------|----------------------|
| 기존 버그 수정 | `/debug` |
| UI 컴포넌트 개발 | 일반 개발 + `/e2e` |
| 전체 커버리지 분석 | `/test-coverage` |
| 고급 테스팅 (Property-based) | `/testing` |

### 혼동하기 쉬운 상황

**Q: `/tdd` vs `/testing`?**
- `/tdd`: RED-GREEN-REFACTOR 사이클
- `/testing`: 다양한 테스트 기법 (Property-based, Mutation 등)

**Q: `/tdd` vs `/debug`?**
- `/tdd`: 새 기능 개발
- `/debug`: 버그 수정 (재현 테스트 먼저)

---

## 🔗 함께 사용하면 좋은 워크플로우

### 새 기능 개발 흐름

```
/write-plan          # 계획 (복잡한 경우)
    ↓
/tdd                 # 핵심 로직 TDD
    ↓
/testing             # 고급 테스트 추가
    ↓
/test-coverage       # 커버리지 확인
    ↓
/code-review         # 품질 검토
```

### 버그 수정 흐름

```
/debug               # 재현 테스트 + 원인 파악
    ↓
/tdd                 # 수정 + 테스트 강화
```

---

## ✅ 체크리스트

### TDD 전

- [ ] 요구사항이 명확한가?
- [ ] 인터페이스가 정의되었는가?

### TDD 중

- [ ] 테스트가 먼저 작성되었는가?
- [ ] 테스트가 실패(RED)하는가?
- [ ] 최소한의 코드로 통과(GREEN)했는가?
- [ ] 리팩토링 후에도 테스트가 통과하는가?

### TDD 후

- [ ] 커버리지 80% 이상인가?
- [ ] Edge case가 테스트되었는가?

---

## 💡 TDD 베스트 프랙티스

**DO:**
- ✅ 한 번에 하나의 테스트만 추가
- ✅ 실패 확인 후 구현
- ✅ 최소 코드로 통과
- ✅ 리팩토링은 테스트 통과 상태에서

**DON'T:**
- ❌ 여러 테스트 한 번에 작성
- ❌ 테스트 없이 구현
- ❌ 과도한 구현 (YAGNI 위반)
- ❌ 실패하는 테스트 방치

### Edge Cases 체크리스트

| 입력 유형 | 테스트 케이스 |
|----------|--------------|
| 숫자 | 0, -1, MAX_INT, NaN, Infinity |
| 문자열 | "", " ", 매우 긴 문자열, unicode |
| 배열 | [], 단일 요소, 최대 크기 |
| 객체 | {}, null, undefined, 중첩 |
