# Session Management Guide

> 100K 토큰 한계를 관리하는 방법

---

## 📌 왜 세션 관리가 필요한가?

Claude Opus 4.5는 컨텍스트가 길어질수록:
- 응답 속도 저하
- 메모리 부정확
- 비용 증가

**권장**: 100K 토큰 접근 시 새 세션 시작

---

## 🔄 Handoff → Pickup 플로우

### 1. Handoff (세션 저장)

작업 중:
```
/handoff
```

생성되는 문서: `.agent/handoffs/YYYY-MM-DD-[slug].md`

### 2. 새 세션 시작

Antigravity에서 새 대화 시작

### 3. Pickup (세션 복원)

```
/pickup [파일명]
```

예: `/pickup 2026-01-21-oauth-auth`

---

## 📤 Handoff 문서 포함 내용

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

## 4. Pending Tasks
- [ ] 미완료 작업

## 5. Current Work
[핸드오프 직전 작업]

## 6. Next Steps
[권장 다음 작업]

## 7. Failed Approaches (중요!)
- [시도했지만 안 된 접근법]
```

---

## 💡 언제 Handoff 해야 하나?

| 상황 | 권장 |
|------|------|
| 2-3시간 연속 작업 | ✅ Handoff |
| 응답이 느려짐 | ✅ Handoff |
| 마일스톤 완료 | ✅ Handoff |
| 간단한 작업 | ❌ 불필요 |

---

## ✅ Best Practices

- 정기적으로 저장 (2-3시간마다)
- 실패한 접근법 꼭 기록 (반복 방지)
- 파일 경로만 기재 (전체 코드 X)
- Pending Tasks 구체적으로

---

## 🔗 관련 워크플로우

- `/handoff` - [상세 가이드](guides/handoff.md)
- `/pickup` - [상세 가이드](guides/pickup.md)
- `/learn` - 세션에서 패턴 추출
