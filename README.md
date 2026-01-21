# dotfiles-for-antigravity

> Antigravity AI 코딩 어시스턴트를 위한 완전한 설정 파일 컬렉션

[everything-claude-code](https://github.com/affaan-m/everything-claude-code)에서 영감을 받아, Antigravity용으로 최적화된 workflows, rules, skills, agents를 제공합니다.

---

## 🚀 Quick Start

### 프로젝트에 적용하기

```bash
# 워크플로우만 복사 (권장)
cp -r dotfiles-for-antigravity/.agent/workflows your-project/.agent/workflows

# 또는 전체 .agent 디렉토리 복사
cp -r dotfiles-for-antigravity/.agent your-project/.agent
```

자세한 내용은 [Quick Start Guide](docs/QUICK-START.md) 참조.

---

## 📁 프로젝트 구조

```
dotfiles-for-antigravity/
├── .agent/
│   └── workflows/           # 슬래시 커맨드 정의
│       ├── plan.md          # /plan - 구현 계획
│       ├── tdd.md           # /tdd - TDD 개발
│       ├── e2e.md           # /e2e - E2E 테스트
│       ├── code-review.md   # /code-review
│       ├── build-fix.md     # /build-fix
│       ├── refactor-clean.md
│       ├── test-coverage.md
│       ├── update-docs.md
│       ├── learn.md         # /learn - 패턴 학습
│       ├── handoff.md       # /handoff - 세션 저장
│       └── pickup.md        # /pickup - 세션 복원
│
├── user-rules/              # 사용자 규칙 (글로벌 설정)
│   ├── default.md           # 기본 규칙
│   ├── rules/               # 상세 규칙
│   │   ├── security.md
│   │   ├── coding-style.md
│   │   ├── testing.md
│   │   ├── git-workflow.md
│   │   ├── patterns.md
│   │   └── session-management.md
│   ├── skills/              # 도메인 지식
│   │   ├── coding-standards.md
│   │   ├── backend-patterns.md
│   │   └── frontend-patterns.md
│   ├── agents/              # 에이전트 가이드
│   │   ├── planner.md
│   │   ├── architect.md
│   │   ├── code-reviewer.md
│   │   └── security-reviewer.md
│   └── contexts/            # 컨텍스트 모드
│       ├── dev.md
│       ├── review.md
│       └── research.md
│
├── docs/                    # 문서
│   ├── QUICK-START.md       # 빠른 시작 가이드
│   ├── WORKFLOW-GUIDE.md    # 워크플로우 상세 가이드
│   ├── SESSION-MANAGEMENT.md # 세션 관리 가이드
│   └── FILTERED.md          # Claude 전용 기능 목록
│
├── _archive/                # 기존 콘텐츠 아카이브
└── .reference/              # 원본 레포지토리 참조
```

---

## 🎯 사용 가능한 워크플로우

| 커맨드 | 설명 |
|--------|------|
| `/plan` | 구현 계획 수립 - 코드 작성 전 확인 대기 |
| `/tdd` | TDD 개발 - RED → GREEN → REFACTOR |
| `/e2e` | Playwright E2E 테스트 생성 |
| `/code-review` | 보안 및 품질 리뷰 |
| `/build-fix` | 빌드 에러 점진적 수정 |
| `/refactor-clean` | 데드 코드 정리 |
| `/test-coverage` | 80%+ 커버리지 달성 |
| `/update-docs` | 문서 동기화 |
| `/learn` | 세션에서 패턴 추출 |
| `/handoff` | 세션 상태 저장 |
| `/pickup` | 이전 세션 복원 |

---

## 💡 세션 관리

**100K 토큰** 초과 시 새 세션 전환 권장:

```
1. /handoff          # 현재 상태 저장
2. 새 세션 시작
3. /pickup [file]    # 상태 복원
```

자세한 내용은 [Session Management Guide](docs/SESSION-MANAGEMENT.md) 참조.

---

## 📋 User Rules

### 핵심 규칙

| 규칙 | 내용 |
|------|------|
| [security.md](user-rules/rules/security.md) | 보안 체크리스트, OWASP Top 10 |
| [coding-style.md](user-rules/rules/coding-style.md) | 불변성, 파일 조직, 에러 핸들링 |
| [testing.md](user-rules/rules/testing.md) | TDD, 80% 커버리지 |
| [session-management.md](user-rules/rules/session-management.md) | 100K 토큰 관리 |

### Skills (도메인 지식)

| 스킬 | 내용 |
|------|------|
| [coding-standards.md](user-rules/skills/coding-standards.md) | TypeScript/JS 표준 |
| [backend-patterns.md](user-rules/skills/backend-patterns.md) | API, DB, 캐싱 패턴 |
| [frontend-patterns.md](user-rules/skills/frontend-patterns.md) | React, Next.js 패턴 |

---

## ⚠️ Claude Code 전용 기능

다음 기능은 Claude Code 전용으로 Antigravity에서는 지원되지 않습니다:

- Hooks (PreToolUse, PostToolUse, Stop)
- MCP Server Configs
- Memory Persistence System
- Strategic Compact

자세한 내용은 [FILTERED.md](docs/FILTERED.md) 참조.

---

## 🤝 Contributing

1. 새 워크플로우: `.agent/workflows/` 에 추가
2. 새 규칙: `user-rules/rules/` 에 추가
3. 새 스킬: `user-rules/skills/` 에 추가

---

## 📄 License

MIT License

---

## 🙏 Credits

- [everything-claude-code](https://github.com/affaan-m/everything-claude-code) - 원본 레포지토리
- Anthropic Hackathon Winner의 프로덕션 레디 설정들
