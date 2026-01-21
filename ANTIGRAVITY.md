# ANTIGRAVITY.md

> 이 파일은 Antigravity AI 에이전트에게 프로젝트 컨텍스트를 제공합니다.
> 다른 프로젝트에 복사 후 내용을 수정하세요.

---

## Project Overview

**프로젝트명**: [프로젝트 이름]
**기술 스택**: [예: Next.js 15, TypeScript, Supabase, Tailwind CSS]
**설명**: [프로젝트가 무엇을 하는지 1-2문장으로]

---

## Essential Commands

```bash
# 개발 서버
npm run dev

# 빌드
npm run build

# 테스트
npm test

# 린트
npm run lint
```

---

## Directory Structure

```
src/
├── app/              # Next.js App Router
├── components/       # React 컴포넌트
├── hooks/            # 커스텀 훅
├── lib/              # 유틸리티
├── types/            # TypeScript 타입
└── styles/           # 스타일
```

---

## Key Files

| 파일 | 설명 |
|------|------|
| `src/app/page.tsx` | 메인 페이지 |
| `src/lib/api.ts` | API 클라이언트 |
| `src/types/index.ts` | 공통 타입 정의 |

---

## Development Guidelines

### Code Style
- 불변성 유지 - 객체/배열 직접 수정 X
- 파일당 200-400줄, 최대 800줄
- 함수당 최대 50줄

### Testing
- TDD: 테스트 먼저 작성
- 80% 이상 커버리지 목표

### Git
- Conventional Commits: `feat:`, `fix:`, `refactor:`, `docs:`, `test:`
- PR 전 로컬 테스트 필수

---

## Available Workflows

```
/plan           # 구현 계획 수립
/tdd            # TDD 개발
/e2e            # E2E 테스트
/code-review    # 코드 리뷰
/build-fix      # 빌드 에러 해결
/handoff        # 세션 상태 저장
/pickup         # 세션 복원
```

---

## Environment Variables

```bash
# .env.example 참조
DATABASE_URL=
API_KEY=
```

---

## Session Management

- 100K 토큰 초과 시 `/handoff` → 새 세션 → `/pickup`
- 복잡한 작업 전 `/plan` 실행
- 문제 해결 후 `/learn`으로 패턴 저장

---

## Notes

[프로젝트 특이사항, 주의사항 등]
