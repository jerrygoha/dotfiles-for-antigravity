# dotfiles-for-antigravity

> Antigravity AI 코딩 어시스턴트를 위한 워크플로우 & 설정 컬렉션

[everything-claude-code](https://github.com/affaan-m/everything-claude-code)에서 영감을 받아, Antigravity + Claude Opus 4.5용으로 최적화됨.

---

## 🚀 Quick Start

### 새 프로젝트에 적용

```bash
# 1. 프로젝트로 이동
cd /path/to/your-project

# 2. 워크플로우 복사
cp -r ~/dotfiles-for-antigravity/.agent/workflows .agent/workflows

# 완료! /write-plan, /tdd, /handoff 등 21개 워크플로우 사용 가능
```

자세한 내용: [Quick Start Guide](docs/QUICK-START.md)

---

## 📁 프로젝트 구조

```
dotfiles-for-antigravity/
├── .agent/workflows/        # 21개 워크플로우 (영문 - LLM용)
│
├── docs/
│   ├── QUICK-START.md       # 시작 가이드
│   ├── WORKFLOW-GUIDE.md    # 워크플로우 인덱스
│   ├── guides/              # 워크플로우별 상세 가이드 (한국어)
│   └── SESSION-MANAGEMENT.md
│
├── user-rules/              # 사용자 규칙 (글로벌 설정)
├── memory-templates/        # 메모리 템플릿
└── _archive/                # 기존 콘텐츠 아카이브
```

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

각 워크플로우 상세 가이드: [WORKFLOW-GUIDE.md](docs/WORKFLOW-GUIDE.md)

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
| `docs/guides/` | 한국어 | 사람이 읽는 가이드 |

---

## 📄 License

MIT License

---

## 🙏 Credits

- [everything-claude-code](https://github.com/affaan-m/everything-claude-code) - 원본 레포지토리
