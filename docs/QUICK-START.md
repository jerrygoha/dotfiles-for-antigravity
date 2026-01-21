# Quick Start Guide

이 프로젝트의 설정을 다른 프로젝트에 적용하는 방법.

---

## 🚀 1분 설정

### 방법 1: Workflows만 복사 (권장)

```bash
# 대상 프로젝트로 이동
cd /path/to/your-project

# workflows 복사
cp -r /path/to/dotfiles-for-antigravity/.agent/workflows .agent/workflows

# 완료! 이제 /plan, /tdd, /handoff 등 사용 가능
```

### 방법 2: 전체 설정 복사

```bash
# 대상 프로젝트로 이동
cd /path/to/your-project

# .agent 디렉토리 전체 복사
cp -r /path/to/dotfiles-for-antigravity/.agent .

# 프로젝트 컨텍스트 파일 복사 (필요시 수정)
cp /path/to/dotfiles-for-antigravity/ANTIGRAVITY.md .
```

---

## 📁 복사되는 파일 구조

```
your-project/
├── .agent/
│   ├── workflows/          # 슬래시 커맨드 정의
│   │   ├── plan.md        # /plan
│   │   ├── tdd.md         # /tdd
│   │   ├── e2e.md         # /e2e
│   │   ├── code-review.md # /code-review
│   │   ├── build-fix.md   # /build-fix
│   │   ├── handoff.md     # /handoff
│   │   ├── pickup.md      # /pickup
│   │   └── ...
│   ├── handoffs/           # 핸드오프 문서 저장
│   └── plans/              # 구현 계획 저장
│
└── ANTIGRAVITY.md          # 프로젝트 컨텍스트 (선택)
```

---

## 🎯 사용 가능한 워크플로우

| 커맨드 | 설명 |
|--------|------|
| `/plan` | 구현 계획 수립 |
| `/tdd` | TDD 개발 워크플로우 |
| `/e2e` | E2E 테스트 생성 |
| `/code-review` | 코드 리뷰 |
| `/build-fix` | 빌드 에러 해결 |
| `/refactor-clean` | 데드 코드 정리 |
| `/test-coverage` | 커버리지 분석 |
| `/update-docs` | 문서 동기화 |
| `/learn` | 패턴 학습 |
| `/handoff` | 세션 상태 저장 |
| `/pickup` | 이전 세션 복원 |

---

## 🔧 ANTIGRAVITY.md 커스터마이징

프로젝트별로 `ANTIGRAVITY.md` 수정:

```markdown
# ANTIGRAVITY.md

## Project Overview
[프로젝트 설명 - 기술 스택, 목적]

## Key Files
[중요 파일 및 디렉토리 설명]

## Development Guidelines
[프로젝트 특정 가이드라인]

## Available Commands
[사용 가능한 스크립트]
```

---

## 👤 글로벌 User Rules (선택)

모든 프로젝트에 적용할 규칙:

```bash
# Antigravity 글로벌 설정에 user-rules 경로 지정
# (Antigravity 설정 방법에 따라 다름)

# user-rules 디렉토리 복사
cp -r dotfiles-for-antigravity/user-rules ~/.config/antigravity/
```

### User Rules 구조

```
user-rules/
├── default.md              # 기본 규칙
├── rules/                  # 상세 규칙
│   ├── security.md
│   ├── coding-style.md
│   ├── testing.md
│   └── session-management.md
├── skills/                 # 도메인 지식
├── agents/                 # 에이전트 가이드
└── contexts/               # 컨텍스트 모드
```

---

## 💡 Tips

### 세션 관리
- 100K 토큰 초과 시 `/handoff` → 새 세션 → `/pickup`
- 복잡한 작업 전 `/plan` 실행
- 문제 해결 후 `/learn`으로 패턴 저장

### 워크플로우 커스터마이징
```markdown
---
description: 내 커스텀 워크플로우
---

# Custom Workflow

[워크플로우 내용]

// turbo
```bash
# 자동 실행 명령
npm run custom-script
```
```

`// turbo` 주석이 있으면 해당 명령 자동 실행.

---

## ❓ FAQ

### Q: 특정 워크플로우만 복사해도 되나요?
A: 네, 필요한 `.md` 파일만 복사해도 됩니다.

### Q: 기존 .agent 폴더가 있으면?
A: `workflows/` 디렉토리만 머지하거나 덮어쓰세요.

### Q: 워크플로우가 인식되지 않아요
A: 파일이 `.agent/workflows/` 경로에 있고, YAML frontmatter가 올바른지 확인하세요.
