# Quick Start Guide

> 새 프로젝트에서 dotfiles 설정을 가져오는 방법

---

## 🚀 새 프로젝트 시작하기

### Step 1: 프로젝트 생성

```bash
# 새 프로젝트 디렉토리 생성
mkdir my-new-project
cd my-new-project
git init
```

### Step 2: dotfiles에서 워크플로우 가져오기

```bash
# 방법 1: workflows만 복사 (최소)
mkdir -p .agent
cp -R ~/dotfiles-for-antigravity/.agent/workflows/. .agent/workflows/

# 방법 2: workflows + 한국어 가이드 (권장)
mkdir -p .agent
cp -R ~/dotfiles-for-antigravity/.agent/workflows/. .agent/workflows/
cp -R ~/dotfiles-for-antigravity/docs/. docs/

# 방법 3: 전체 복사 (프로젝트 컨텍스트 포함)
cp -R ~/dotfiles-for-antigravity/.agent/. .agent/
cp -R ~/dotfiles-for-antigravity/docs/. docs/
cp ~/dotfiles-for-antigravity/ANTIGRAVITY.md .
```

### Step 3: 확인

```bash
ls -la .agent/workflows/
# 21개 워크플로우 파일이 보이면 완료!
```

---

## 📁 복사되는 구조

```
your-project/
├── .agent/
│   └── workflows/           # 21개 워크플로우
│       ├── write-plan.md    # /write-plan
│       ├── execute-plan.md  # /execute-plan
│       ├── tdd.md           # /tdd
│       ├── debug.md         # /debug
│       ├── code-review.md   # /code-review
│       ├── handoff.md       # /handoff
│       ├── pickup.md        # /pickup
│       └── ...
│
└── ANTIGRAVITY.md           # 프로젝트 컨텍스트 (선택)
```

---

## 🎯 사용 가능한 워크플로우 (21개)

### 계획 & 실행
| 커맨드 | 설명 |
|--------|------|
| `/write-plan` | 구현 계획 수립 |
| `/execute-plan` | 계획 단계별 실행 |
| `/brainstorm` | 아이디어 탐색 & 비교 |

### 테스트 & 디버깅
| 커맨드 | 설명 |
|--------|------|
| `/tdd` | RED-GREEN-REFACTOR 개발 |
| `/testing` | 고급 테스팅 기법 |
| `/e2e` | Playwright E2E 테스트 |
| `/test-coverage` | 커버리지 분석 |
| `/debug` | TDD 기반 디버깅 |

### 리뷰 & 정리
| 커맨드 | 설명 |
|--------|------|
| `/code-review` | 보안 및 품질 리뷰 |
| `/refactor-clean` | 데드 코드 정리 |
| `/fix-ci` | CI/CD 실패 해결 |

### 문서화 & 학습
| 커맨드 | 설명 |
|--------|------|
| `/research` | 다중 출처 기술 조사 |
| `/learn` | 패턴 추출 & 저장 |
| `/update-docs` | 문서 자동 생성 |
| `/update-codemaps` | 아키텍처 문서화 |

### Git & 세션 관리
| 커맨드 | 설명 |
|--------|------|
| `/git-workflow` | 브랜치, 커밋 관리 |
| `/git-exclude` | 로컬 전용 ignore |
| `/create-pr` | PR 생성 |
| `/handoff` | 세션 상태 저장 |
| `/pickup` | 세션 복원 |

### 유틸리티
| 커맨드 | 설명 |
|--------|------|
| `/create-workflow` | 새 워크플로우 생성 |

---

## 🔧 ANTIGRAVITY.md 커스터마이징

프로젝트별로 `ANTIGRAVITY.md` 수정:

```markdown
# Project: [프로젝트 이름]

## Overview
[프로젝트 설명, 기술 스택]

## Key Files
- `src/` - 소스 코드
- `tests/` - 테스트 파일

## Commands
- `npm run dev` - 개발 서버
- `npm test` - 테스트 실행

## Guidelines
- [프로젝트 특정 가이드라인]
```

---

## 💡 Tips

### 세션 관리
- 100K 토큰 초과 예상 시 → `/handoff` → 새 세션 → `/pickup`
- 복잡한 작업 전 `/write-plan` 실행
- 문제 해결 후 `/learn`으로 패턴 저장

### 일반 팁
- 워크플로우는 영어로 작성됨 (LLM 컨텍스트 절약)
- 한국어 가이드는 `docs/guides/`에서 확인

---

## ❓ FAQ

### Q: 특정 워크플로우만 복사해도 되나요?
A: 네, 필요한 `.md` 파일만 복사하세요.

### Q: 기존 .agent 폴더가 있으면?
A: `workflows/` 디렉토리만 머지하거나 덮어쓰세요.

### Q: 워크플로우가 인식되지 않아요
A: 파일이 `.agent/workflows/` 경로에 있고, YAML frontmatter가 올바른지 확인하세요.

### Q: dotfiles 경로를 모르겠어요
A: 일반적으로 `~/dotfiles-for-antigravity/` 또는 클론한 위치입니다.
