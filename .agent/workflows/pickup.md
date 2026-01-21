---
description: Restore session context from handoff document
---

# Pickup Workflow

이전 세션의 핸드오프 문서를 읽고 컨텍스트를 복원합니다.

## When to Use

- 새 세션에서 이전 작업 이어할 때
- `/handoff`로 저장한 상태 복원 시

---

## Process

### 1. 핸드오프 문서 확인

// turbo
```bash
ls -la .agent/handoffs/*.md 2>/dev/null || echo "No handoffs found"
```

### 2. 문서 읽기

```
/pickup [filename]
```

예: `/pickup 2026-01-21-implement-auth`

### 3. 컨텍스트 복원 확인

핸드오프 문서 읽은 후:
- Pending Tasks 확인
- Current Work 파악
- Next Steps 검토

---

## Output

```markdown
## 세션 컨텍스트 복원 완료

### 이전 작업 요약
[요약 내용]

### 다음 작업
1. [작업 1]
2. [작업 2]

### 관련 파일
- [파일 목록]

이어서 작업할까요?
```

---

## Best Practices

- ✅ 핸드오프 문서 전체 읽기
- ✅ Pending Tasks부터 시작
- ✅ 이전 실패 접근법 확인
- ❌ 핸드오프 없이 추측으로 이어가기 X

---

## Related

- `/handoff` - 세션 컨텍스트 저장
