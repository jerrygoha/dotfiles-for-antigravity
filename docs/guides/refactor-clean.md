# /refactor-clean 완벽 상세 가이드

> 데드 코드를 식별하고 안전하게 제거하는 워크플로우

---

## 📌 개요 및 목적

`/refactor-clean`은 **사용되지 않는 코드를 식별**하고 테스트를 통해 안전하게 제거하는 워크플로우입니다.

---

## 🎯 언제 사용하나요?

### ✅ 이럴 때 사용하세요

| 상황 | 예시 |
|------|------|
| 기술 부채 정리 | "안 쓰는 코드 정리" |
| 리팩토링 후 정리 | "이전 코드 삭제" |
| 의존성 정리 | "안 쓰는 패키지 제거" |
| 프로젝트 정리 | "전체 코드베이스 정리" |

---

## 📤 기대 결과물

### 분석 리포트

```markdown
## Dead Code Analysis

### 🟢 SAFE (자동 삭제 가능)
- `src/utils/deprecated.ts` - 참조 없음
- `src/components/OldButton.tsx` - import 없음

### 🟡 CAUTION (수동 확인 필요)
- `src/api/legacy.ts` - 동적 import 가능성

### 🔴 DANGER (삭제 금지)
- `src/config/index.ts` - 설정 파일
```

### 정리 결과

```markdown
## Cleanup Summary

### Removed Files
- src/utils/deprecated.ts
- src/components/OldButton.tsx

### Removed Dependencies
- lodash-es (unused)
- moment (replaced by dayjs)

### Tests: All Passing ✅
```

---

## 📖 상세 사용법

### Step 1: 호출

```
/refactor-clean
```

### Step 2: 분석 결과 확인

SAFE, CAUTION, DANGER 레벨 확인

### Step 3: 삭제 승인

```
"SAFE 레벨 모두 삭제해줘"
"CAUTION 중에 legacy.ts도 삭제해"
```

### Step 4: 테스트 확인

자동으로 테스트 실행하여 검증

---

## ⚠️ 이런 상황엔 다른 워크플로우를!

| 상황 | 대신 사용할 워크플로우 |
|------|----------------------|
| 로직 수정 | `/debug` 또는 일반 개발 |
| 테스트 부족 | `/test-coverage` 먼저 |
| 아키텍처 변경 | `/write-plan` 먼저 |

---

## 🔗 함께 사용하면 좋은 워크플로우

```
/test-coverage       # 테스트 보강
    ↓
/refactor-clean      # 데드 코드 정리
    ↓
/code-review         # 최종 검토
```

---

## ✅ 안전한 정리 체크리스트

- [ ] 테스트가 통과하는 상태에서 시작
- [ ] SAFE 레벨만 자동 삭제
- [ ] CAUTION은 수동 확인
- [ ] DANGER는 절대 삭제 X
- [ ] 삭제 후 테스트 재실행

---

## 💡 프로 팁

1. **테스트 먼저**: 테스트 커버리지 확보 후 정리
2. **작은 단위**: 한 번에 많이 삭제 X
3. **커밋 분리**: 정리 커밋은 기능 커밋과 분리
4. **동적 사용 주의**: `import()`, `require()` 확인
