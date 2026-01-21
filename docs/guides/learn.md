# /learn 완벽 상세 가이드

> 세션에서 해결한 문제의 패턴을 추출하고 저장하는 워크플로우

---

## 📌 개요 및 목적

`/learn`은 현재 세션에서 **해결한 문제의 패턴을 추출**하여 나중에 재사용할 수 있도록 저장하는 워크플로우입니다.

---

## 🎯 언제 사용하나요?

### ✅ 이럴 때 사용하세요

| 상황 | 예시 |
|------|------|
| 복잡한 버그 해결 후 | "이 해결법 기록해둬" |
| 유용한 패턴 발견 | "이 패턴 나중에도 쓸 것 같아" |
| 라이브러리 quirk | "이 라이브러리 특이사항" |
| 워크어라운드 | "임시 해결책 문서화" |

### ❌ 사용하지 않을 때

- 오타 수정 같은 단순 변경
- 일반적인 코딩 패턴
- 이미 문서화된 내용

---

## 📤 기대 결과물

### 생성 파일

**위치**: `.agent/learnings/[pattern-name].md`

### 문서 구조

```markdown
# Next.js Hydration Mismatch 해결

**Extracted:** 2026-01-21
**Context:** SSR과 CSR 간 불일치 문제

## Problem
useEffect 없이 window 객체 접근 시 Hydration 에러

## Solution
```typescript
const [mounted, setMounted] = useState(false)

useEffect(() => {
  setMounted(true)
}, [])

if (!mounted) return null
```

## When to Use
- window, document 접근 시
- localStorage 사용 시
- 브라우저 전용 API 사용 시

## Related Files
- src/hooks/useHydration.ts

## Tags
#next.js #hydration #ssr
```

---

## 📖 상세 사용법

### Step 1: 문제 해결 완료 후 호출

```
/learn
```

또는

```
/learn 방금 해결한 Hydration 에러 패턴 저장해줘
```

### Step 2: 패턴 검토

에이전트가 추출한 패턴 확인

### Step 3: 보완 (필요시)

```
"When to Use에 timezone 관련도 추가해줘"
```

### Step 4: 저장 확인

```bash
ls -la .agent/learnings/
```

---

## ⚠️ 이런 상황엔 다른 워크플로우를!

| 상황 | 대신 사용할 워크플로우 |
|------|----------------------|
| 세션 상태 저장 | `/handoff` |
| 문서 업데이트 | `/update-docs` |
| 코드 리뷰 | `/code-review` |

### `/learn` vs `/handoff`

- `/learn`: 범용 패턴 저장 (다른 프로젝트에도 적용 가능)
- `/handoff`: 현재 세션 상태 저장 (이 프로젝트 전용)

---

## 🔗 함께 사용하면 좋은 워크플로우

```
/debug               # 버그 해결
    ↓
/learn               # 패턴 추출
    ↓
/code-review         # 최종 검토
```

---

## ✅ 좋은 학습 패턴 체크리스트

- [ ] Problem이 명확한가?
- [ ] Solution이 재현 가능한가?
- [ ] When to Use가 구체적인가?
- [ ] 코드 예시가 있는가?

---

## 💡 프로 팁

1. **즉시 기록**: 해결 직후가 가장 정확
2. **범용적으로**: 이 프로젝트만이 아닌 다른 프로젝트에도 적용 가능하게
3. **태그 활용**: 나중에 검색 가능하도록
4. **정기 검토**: 오래된 패턴 업데이트
