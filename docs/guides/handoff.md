# /handoff 완벽 상세 가이드

> 세션 컨텍스트를 저장하여 새 세션에서 이어가는 워크플로우

---

## 📌 개요 및 목적

`/handoff`는 현재 세션의 **작업 상태를 저장**하여 새 세션에서 이어서 작업할 수 있게 하는 워크플로우입니다.

**왜 필요한가요?**
- 100K+ 토큰 세션은 성능 저하
- 장시간 작업 중간 저장
- 다른 사람이 이어받을 수 있음

---

## 🎯 언제 사용하나요?

### ✅ 이럴 때 사용하세요

| 상황 | 예시 |
|------|------|
| 100K 토큰 초과 예상 | 장시간 복잡한 작업 |
| 작업 중단 | "오늘은 여기까지" |
| 마일스톤 완료 | "Phase 1 끝" |
| 복잡한 디버깅 | 진행 상황 보존 필요 |

### ⏰ Handoff 타이밍

- 2-3시간 연속 작업 후
- 세션 응답이 느려질 때
- 중요 마일스톤 달성 시

---

## 📤 기대 결과물

### 생성 파일

**위치**: `.agent/handoffs/YYYY-MM-DD-[slug].md`

### 문서 구조

```markdown
# OAuth 인증 시스템 구현 진행 상황

## 1. Primary Request and Intent
소셜 로그인(Google, GitHub) 기능 구현

## 2. Key Technical Concepts
- NextAuth.js 사용
- Prisma 어댑터 연동
- 세션 기반 인증

## 3. Files and Code Sections
### src/app/api/auth/[...nextauth]/route.ts
- **Why important**: 인증 핵심 로직
- **Changes made**: Google Provider 추가

### src/lib/prisma.ts
- **Changes made**: User 모델 확장

## 4. Problem Solving
- [해결] Google OAuth callback URL 설정
- [진행중] GitHub OAuth 연동

## 5. Pending Tasks
- [ ] GitHub OAuth 완료
- [ ] 비밀번호 재설정 기능

## 6. Current Work
GitHub OAuth Provider 설정 진행 중

## 7. Next Steps
1. GitHub OAuth 완료
2. 비밀번호 재설정 이메일 연동
3. 프로필 페이지 구현
```

---

## 📖 상세 사용법

### Step 1: 호출

```
/handoff
```

### Step 2: 문서 검토

생성된 핸드오프 문서를 확인

### Step 3: 보완 요청 (필요시)

```
"실패했던 접근법도 추가해줘"
```

### Step 4: 새 세션에서 복원

```
/pickup 2026-01-21-oauth-auth
```

---

## ⚠️ 이런 상황엔 다른 워크플로우를!

| 상황 | 대신 사용할 워크플로우 |
|------|----------------------|
| 패턴/학습 저장 | `/learn` |
| 간단한 작업 | 핸드오프 불필요 |
| 계획만 저장 | `/write-plan` 후 종료 |

---

## 🔗 함께 사용하면 좋은 워크플로우

### 장시간 프로젝트 흐름

```
/write-plan          # 전체 계획
    ↓
Phase 1 작업
    ↓
/handoff             # 중간 저장
    ↓
(새 세션)
    ↓
/pickup              # 복원
    ↓
Phase 2 계속
```

---

## ✅ 좋은 핸드오프 체크리스트

- [ ] 현재 작업 상태가 명확한가?
- [ ] Pending Tasks가 구체적인가?
- [ ] 실패한 접근법이 기록됐는가?
- [ ] 파일 경로가 정확한가?
- [ ] Next Steps가 명확한가?

---

## 💡 프로 팁

1. **정기적 저장**: 2-3시간마다
2. **간결하게**: 파일 내용 복사 X, 경로만
3. **실패도 기록**: 다시 시도 방지
4. **바로 확인**: 생성 후 읽어보기
