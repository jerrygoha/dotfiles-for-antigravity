# /write-plan 가이드

> 복잡한 기능 구현 전 체계적인 계획을 수립하는 워크플로우

---

## 📌 언제 사용하나요?

| 상황 | 예시 |
|------|------|
| 2시간 이상 소요 예상 | "사용자 인증 시스템 추가" |
| 여러 파일 수정 필요 | "결제 시스템 통합" |
| 리스크가 있는 작업 | "DB 마이그레이션" |
| 팀 협업 필요 | "API 구조 변경" |

---

## 📤 결과물

**저장 위치**: `.agent/plans/YYYY-MM-DD-[feature].md`

### 계획서 구조

```markdown
# [기능명]

## Problem Statement
[해결하려는 문제]

## Goals / Non-Goals
- 목표와 명시적 범위 외 항목

## Technical Approach
- 아키텍처, 영향받는 컴포넌트

## Implementation Steps
- Phase 1, 2, ... (각 30분~2시간 단위)

## Risk Assessment
- P×I 점수로 리스크 정량화

## Testing Strategy / Rollback Plan
```

---

## 💡 사용법

```
/write-plan OAuth 인증 기능을 추가하고 싶어.
Google, GitHub 로그인, 비밀번호 재설정 필요해.
```

---

## ⚠️ 이럴 땐 다른 워크플로우!

| 상황 | 대신 사용 |
|------|----------|
| 아이디어 탐색 단계 | `/brainstorm` |
| 기술 조사 필요 | `/research` |
| 간단한 버그 수정 | 바로 수정 또는 `/debug` |

---

## 🔗 권장 흐름

```
/research (필요시) → /brainstorm (옵션) → /write-plan → /execute-plan
```
