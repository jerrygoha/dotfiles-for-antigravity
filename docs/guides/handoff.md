# /handoff 가이드

> 세션 컨텍스트를 저장하여 새 세션에서 이어가는 워크플로우

---

## 📌 언제 사용하나요?

| 상황 | 예시 |
|------|------|
| 100K+ 토큰 접근 | 세션이 길어짐 |
| 복잡한 디버깅 중 | 진행 상황 보존 필요 |
| 마일스톤 완료 | Phase 1 끝 |
| 작업 중단 | "오늘은 여기까지" |

---

## 📤 핸드오프 문서 구조

**저장 위치**: `.agent/handoffs/YYYY-MM-DD-[slug].md`

```markdown
# [작업 요약]

## 1. Primary Request and Intent
[원래 요청 및 목표]

## 2. Key Technical Concepts
- 핵심 개념들

## 3. Files and Code Sections
### [파일명]
- **Why important**: [이유]
- **Changes made**: [변경사항]

## 4. Problem Solving
[해결한 문제 및 진행 중인 트러블슈팅]

## 5. Pending Tasks
- [ ] 미완료 작업들

## 6. Current Work
[핸드오프 직전 작업 중이던 내용]

## 7. Next Steps
[권장 다음 작업]

## 8. Failed Approaches (중요!)
- [시도했지만 안 된 접근법과 이유]
```

---

## ✅ 반드시 포함할 것

- 주요 목표와 컨텍스트
- 파일 경로 (전체 코드 X)
- 명확한 Pending Tasks
- **실패한 접근법** (반복 방지!)

---

## 🔗 관련 워크플로우

- `/pickup` - 핸드오프 문서로 세션 복원
- `/learn` - 세션에서 패턴 추출
