---
description: Save session context for continuation in new session (100K+ tokens)
---

# Handoff Workflow

세션 컨텍스트를 저장하여 새 세션에서 이어서 작업할 수 있게 합니다.

## When to Use

- 100K 토큰 초과 예상 시
- 장시간 작업 중단 시
- 마일스톤 완료 시
- 복잡한 디버깅 진행 중

---

## Process

### 1. 핸드오프 문서 생성

Save to: `.agent/handoffs/YYYY-MM-DD-[slug].md`

### 2. 문서 구조

```markdown
# [Readable Summary]

## 1. Primary Request and Intent
[사용자의 원래 요청 및 의도]

## 2. Key Technical Concepts
- [핵심 개념 1]
- [핵심 개념 2]

## 3. Files and Code Sections
### [파일명]
- **Why important**: [중요한 이유]
- **Changes made**: [변경 사항]

## 4. Problem Solving
[해결한 문제 및 진행 중인 트러블슈팅]

## 5. Pending Tasks
- [ ] 미완료 작업 1
- [ ] 미완료 작업 2

## 6. Current Work
[핸드오프 직전 작업 중이던 내용]

## 7. Next Steps
[권장 다음 작업]
```

---

## Best Practices

- ✅ 중요 결정 사항 기록
- ✅ 실패한 접근법도 기록 (반복 방지)
- ✅ 파일 경로 명확히 기재
- ❌ 전체 코드 복사 X (경로만 기재)

---

## Related

- `/pickup` - 핸드오프 문서로 세션 복원
- `/learn` - 세션에서 패턴 추출
