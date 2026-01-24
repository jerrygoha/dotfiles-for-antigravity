# dotfiles-for-antigravity

> Antigravity AI 코딩 어시스턴트를 위한 워크플로우 & 스킬 컬렉션

[everything-claude-code](https://github.com/affaan-m/everything-claude-code)에서 영감을 받아, Antigravity + Claude Opus 4.5용으로 최적화됨.

---

## 🚀 Quick Start

### 새 프로젝트에 적용

```bash
# 1. 프로젝트로 이동
cd /path/to/your-project

# 2. 방법 선택

# 방법 1: 최소 (workflows만)
cp -R ~/dotfiles-for-antigravity/.agent/workflows/. .agent/workflows/

# 방법 2: 권장 (workflows + skills) ⭐
cp -R ~/dotfiles-for-antigravity/.agent/. .agent/

# 방법 3: 전체 (workflows + skills + 문서)
cp -R ~/dotfiles-for-antigravity/.agent/. .agent/
cp -R ~/dotfiles-for-antigravity/docs/. docs/
```

자세한 내용: [Quick Start Guide](docs/QUICK-START.md)

---

## 📁 프로젝트 구조

```
dotfiles-for-antigravity/
├── .agent/
│   ├── workflows/        # 21개 워크플로우 (영문 - LLM용)
│   └── skills/           # 9개 스킬 (도메인 지식)
│       ├── backend-patterns/
│       ├── clickhouse-io/
│       ├── coding-standards/
│       ├── continuous-learning/
│       ├── frontend-patterns/
│       ├── project-guidelines/
│       ├── security-review/
│       ├── strategic-compact/
│       └── tdd-workflow/
│
├── docs/
│   ├── QUICK-START.md       # 시작 가이드
│   ├── WORKFLOW-GUIDE.md    # 워크플로우 인덱스
│   ├── SKILLS-GUIDE.md      # 스킬 인덱스
│   ├── SKILLS-SETUP.md      # 스킬 설정 가이드
│   └── guides/              # 워크플로우별 가이드 (한국어)
│
├── user-rules/              # 사용자 규칙 (글로벌 설정)
└── memory-templates/        # 메모리 템플릿
```

---

## 🧠 스킬 (9개)

모든 스킬은 폴더 구조로 통일되어 자동 활성화됩니다.

| 스킬 | 설명 |
|------|------|
| `coding-standards/` | TypeScript/JS 코딩 표준 |
| `backend-patterns/` | API, DB, 캐싱 패턴 |
| `frontend-patterns/` | React, Next.js 패턴 |
| `clickhouse-io/` | ClickHouse 분석 DB 패턴 |
| `security-review/` | 보안 체크리스트 |
| `tdd-workflow/` | TDD 개발 가이드 |
| `project-guidelines/` | 프로젝트 가이드라인 템플릿 |
| `continuous-learning/` | 세션 패턴 자동 추출 |
| `strategic-compact/` | 전략적 컴팩트 제안 |

📖 상세 가이드: [SKILLS-GUIDE.md](docs/SKILLS-GUIDE.md)

---

## 🎯 워크플로우 목록 (21개)

| 카테고리 | 워크플로우 |
|----------|-----------| 
| **계획** | `/write-plan`, `/execute-plan`, `/brainstorm` |
| **테스트** | `/tdd`, `/testing`, `/e2e`, `/test-coverage`, `/debug` |
| **리뷰** | `/code-review`, `/refactor-clean`, `/fix-ci` |
| **문서** | `/research`, `/learn`, `/update-docs`, `/update-codemaps` |
| **Git** | `/git-workflow`, `/git-exclude`, `/create-pr` |
| **세션** | `/handoff`, `/pickup` |
| **유틸** | `/create-workflow` |

📖 상세 가이드: [WORKFLOW-GUIDE.md](docs/WORKFLOW-GUIDE.md)

---

## 💡 핵심 사용법

### 새 기능 개발
```
/write-plan → /execute-plan → /tdd → /code-review → /create-pr
```

### 버그 수정
```
/debug → /tdd (테스트 보강) → /learn (패턴 기록)
```

### 세션 관리 (100K+ 토큰)
```
/handoff → 새 세션 → /pickup
```

---

## 📋 파일 구분

| 파일 유형 | 언어 | 용도 |
|----------|------|------|
| `.agent/workflows/` | 영문 | LLM 컨텍스트 절약 |
| `.agent/skills/` | 영문 | 도메인 지식 (자동 활성화) |
| `docs/guides/` | 한국어 | 사람이 읽는 가이드 |

---

## 📄 License

MIT License

---

## 🙏 Credits

- [everything-claude-code](https://github.com/affaan-m/everything-claude-code) - 원본 레포지토리
