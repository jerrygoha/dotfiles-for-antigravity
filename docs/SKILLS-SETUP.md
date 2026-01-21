# Antigravity Skills 설정 가이드

> Antigravity에서 글로벌/프로젝트 스킬을 사용하는 방법

---

## 📌 스킬이란?

스킬은 AI에게 특정 도메인 지식을 제공하는 참조 문서입니다. 워크플로우와 달리 **자동으로 활성화**되어 관련 작업 시 활용됩니다.

---

## 🔧 Antigravity 스킬 경로

### 글로벌 스킬 (모든 프로젝트에 적용)

**버그 수정 필요!** 구글이 경로를 잘못 설정함:

```bash
# 심볼릭 링크로 해결 (macOS/Linux/WSL)
ln -s ~/.gemini/antigravity/skills ~/.gemini/antigravity/global_skills

# 또는 global_skills 폴더에 직접 배치
mkdir -p ~/.gemini/antigravity/global_skills
cp -r ~/dotfiles-for-antigravity/.reference/everything-claude-code/skills/* ~/.gemini/antigravity/global_skills/
```

### 프로젝트 스킬 (특정 프로젝트에만 적용)

```bash
# 프로젝트 루트에 .agent/skills/ 생성
mkdir -p .agent/skills
cp -r ~/dotfiles-for-antigravity/.reference/everything-claude-code/skills/* .agent/skills/
```

---

## 📁 사용 가능한 스킬 (everything-claude-code 기준)

| 스킬 | 설명 |
|------|------|
| `coding-standards.md` | TypeScript/JS 코딩 표준 |
| `backend-patterns.md` | API, DB, 캐싱 패턴 |
| `frontend-patterns.md` | React, Next.js 패턴 |
| `tdd-workflow/SKILL.md` | TDD 상세 가이드 |
| `security-review/` | 보안 리뷰 스킬 |
| `clickhouse-io.md` | ClickHouse DB 패턴 |

---

## 📤 스킬 파일 형식

### 단일 파일 스킬

```markdown
---
name: skill-name
description: 이 스킬이 활성화되는 상황
---

# 스킬 제목

[스킬 내용]
```

### 폴더 스킬

```
skill-folder/
└── SKILL.md    # 필수: 메인 스킬 파일
```

---

## 🚀 Quick Setup

### 방법 1: 글로벌 스킬 (모든 프로젝트에 적용)

```bash
# 1. 경로 버그 수정
ln -s ~/.gemini/antigravity/skills ~/.gemini/antigravity/global_skills

# 2. 스킬 복사
mkdir -p ~/.gemini/antigravity/skills
cp -r ~/dotfiles-for-antigravity/.reference/everything-claude-code/skills/* ~/.gemini/antigravity/skills/
```

### 방법 2: 프로젝트 스킬 (권장 - dotfiles에 포함시켜 배포)

```bash
# dotfiles에 스킬 추가
mkdir -p ~/dotfiles-for-antigravity/.agent/skills
cp -r ~/dotfiles-for-antigravity/.reference/everything-claude-code/skills/* ~/dotfiles-for-antigravity/.agent/skills/

# 새 프로젝트에 적용 시
cp -r ~/dotfiles-for-antigravity/.agent/skills .agent/skills
```

---

## 💡 프로젝트에 스킬 함께 배포하기

### dotfiles 구조 업데이트

```
dotfiles-for-antigravity/
├── .agent/
│   ├── workflows/    # 워크플로우 (21개)
│   └── skills/       # 스킬 추가! 
│       ├── coding-standards.md
│       ├── backend-patterns.md
│       ├── frontend-patterns.md
│       └── tdd-workflow/
│           └── SKILL.md
```

### 새 프로젝트 시작 시

```bash
# workflows + skills 복사
cp -r ~/dotfiles-for-antigravity/.agent .

# 또는 선택적 복사
cp -r ~/dotfiles-for-antigravity/.agent/workflows .agent/workflows
cp -r ~/dotfiles-for-antigravity/.agent/skills .agent/skills
```

---

## ✅ 확인 방법

스킬이 제대로 로드되면 관련 작업 시 자동 활성화됩니다.
예: TDD 관련 작업 시 `tdd-workflow` 스킬이 자동 적용
