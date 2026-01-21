# /update-codemaps 완벽 상세 가이드

> 코드베이스 구조를 분석하고 아키텍처 문서를 자동 생성하는 워크플로우

---

## 📌 개요 및 목적

`/update-codemaps`는 **코드베이스 구조를 분석**하여 아키텍처 문서를 자동 생성하는 워크플로우입니다.

---

## 🎯 언제 사용하나요?

### ✅ 이럴 때 사용하세요

| 상황 | 예시 |
|------|------|
| 프로젝트 파악 | "전체 구조 파악하고 싶어" |
| 아키텍처 문서화 | "구조 문서 필요" |
| 정기 업데이트 | "주간 코드맵 갱신" |
| 리팩토링 전 | "현재 상태 기록" |

---

## 📤 기대 결과물

### codemaps/architecture.md

```markdown
# Project Architecture

## Directory Structure
src/
├── app/           # Next.js App Router
│   ├── api/       # API routes (15 endpoints)
│   └── (auth)/    # Auth pages
├── components/    # React components (42 files)
├── hooks/         # Custom hooks (8 files)
└── lib/           # Utilities (12 files)

## Key Dependencies
- next → app/, pages/
- supabase → lib/db.ts, api/
- zod → api/, lib/validation.ts

## Data Flow
Request → API Route → Service → Repository → Database
```

---

## 📖 상세 사용법

### Step 1: 호출

```
/update-codemaps
```

### Step 2: 분석 결과 확인

### Step 3: 문서 저장 확인

---

## ⚠️ 이런 상황엔 다른 워크플로우를!

| 상황 | 대신 사용할 워크플로우 |
|------|----------------------|
| 개발자 온보딩 문서 | `/update-docs` |
| API 문서 | 별도 API 문서 도구 |

---

## 🔗 함께 사용하면 좋은 워크플로우

```
/update-codemaps     # 구조 파악
    ↓
/write-plan          # 변경 계획
    ↓
/execute-plan        # 실행
```

---

## 💡 프로 팁

1. **정기적으로**: 주 1회 업데이트 권장
2. **변경 30% 초과**: 사용자 승인 요청
3. **리팩토링 전**: 현재 상태 스냅샷 생성
