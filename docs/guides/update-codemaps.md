# /update-codemaps 가이드

> 코드베이스 구조를 분석하고 아키텍처 문서를 자동 생성하는 워크플로우

---

## 📌 언제 사용하나요?

- 새 코드베이스 파악
- 아키텍처 문서화
- 주간 문서 업데이트
- 대규모 리팩토링 전

---

## 📤 생성되는 문서

**저장 위치**: `codemaps/architecture.md`

```markdown
# Project Architecture

## Directory Structure
src/
├── app/           # Next.js App Router
├── components/    # React 컴포넌트
├── hooks/         # Custom hooks
└── lib/           # 유틸리티

## Key Dependencies
- next → app/, pages/
- supabase → lib/db/

## Data Flow
Request → API Route → Service → Repository → DB

## Patterns Used
- API: Zod validation
- State: React Query / Zustand
```

---

## ✅ 베스트 프랙티스

- ✅ 주 1회 업데이트 권장
- ✅ 의존성 관계 포함
- ✅ 패턴과 컨벤션 문서화
- ❌ 모든 파일 문서화 (고수준만)
- ❌ 코드 주석과 중복 금지

---

## 🔗 권장 흐름

```
/update-codemaps (구조 파악) → /write-plan (변경 계획)
```
