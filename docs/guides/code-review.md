# /code-review 완벽 상세 가이드

> 커밋 전 보안 및 품질을 검토하는 워크플로우

---

## 📌 개요 및 목적

`/code-review`는 변경된 코드의 **보안 취약점**과 **품질 이슈**를 커밋 전에 검토하는 워크플로우입니다.

**검토 항목:**
- 🔴 CRITICAL: 보안 취약점 (하드코딩된 키, SQL Injection 등)
- 🟠 HIGH: 품질 이슈 (에러 핸들링 누락, 긴 함수 등)
- 🟡 MEDIUM: 베스트 프랙티스 (불변성, 테스트 누락 등)
- 🟢 LOW: 스타일 (네이밍, 포맷팅 등)

---

## 🎯 언제 사용하나요?

### ✅ 이럴 때 사용하세요

| 상황 | 예시 |
|------|------|
| 커밋/PR 전 | "푸시하기 전에 검토해줘" |
| 보안 점검 | "보안 취약점 확인" |
| 품질 체크 | "코드 스멜 있는지 봐줘" |
| 팀 리뷰 전 사전 점검 | "셀프 리뷰 도와줘" |

---

## 📤 기대 결과물

```markdown
## Code Review Report

### 🔴 CRITICAL (즉시 수정)

#### src/api/auth.ts:25
**Issue**: 하드코딩된 API 키
**Why**: 소스 코드 노출 시 키 유출
**Fix**:
```typescript
// Before
const API_KEY = "sk-xxxxx"

// After
const API_KEY = process.env.API_KEY
if (!API_KEY) throw new Error('API_KEY required')
```

### 🟠 HIGH

#### src/utils/calc.ts:42
**Issue**: 에러 핸들링 누락
...

## Summary
- CRITICAL: 1 (❌ 커밋 금지)
- HIGH: 2
- MEDIUM: 3
- LOW: 1

**Recommendation**: CRITICAL 수정 후 다시 /code-review
```

---

## 📖 상세 사용법

### Step 1: 호출

```
/code-review
```

또는 특정 디렉토리만:
```
/code-review src/api/
```

### Step 2: 결과 확인

심각도별로 이슈 확인

### Step 3: 수정

CRITICAL, HIGH 순서로 수정

### Step 4: 재검토

```
/code-review
```

CRITICAL/HIGH 없으면 커밋 진행

---

## ⚠️ 이런 상황엔 다른 워크플로우를!

| 상황 | 대신 사용할 워크플로우 |
|------|----------------------|
| 빌드 에러 | `/fix-ci` |
| 테스트 실패 | `/debug` 또는 `/testing` |
| 아키텍처 리뷰 | `/brainstorm` |
| PR 생성 | `/create-pr` (리뷰 후) |

---

## 🔗 함께 사용하면 좋은 워크플로우

```
코드 작성 완료
    ↓
/code-review         # 품질 검토
    ↓
수정
    ↓
/testing             # 테스트 확인
    ↓
/create-pr           # PR 생성
```

---

## ✅ 보안 체크리스트

- [ ] 하드코딩된 시크릿 없음
- [ ] SQL Injection 취약점 없음
- [ ] XSS 취약점 없음
- [ ] 모든 입력 유효성 검사됨
- [ ] 에러 메시지에 민감 정보 없음
- [ ] HTTPS 강제
- [ ] Rate limiting 적용

---

## 💡 프로 팁

1. **자주 실행**: 작은 단위로 자주 리뷰
2. **CRITICAL 우선**: 보안 이슈 최우선
3. **자동화 연계**: CI에 린트/보안 스캔 추가
4. **학습 기회**: 발견된 이슈 패턴 기록
