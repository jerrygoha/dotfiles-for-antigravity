# Antigravity Skills 설정 가이드

> Antigravity에서 글로벌/프로젝트 스킬을 사용하는 방법

---

## 📌 스킬이란?

스킬은 AI에게 특정 도메인 지식을 제공하는 참조 문서입니다. 워크플로우와 달리 **자동으로 활성화**되어 관련 작업 시 활용됩니다.

---

## 📁 사용 가능한 스킬 (9개)

모든 스킬은 폴더 구조로 통일되어 있습니다:

| 스킬 | 설명 |
|------|------|
| `backend-patterns/` | API, DB, 캐싱 패턴 |
| `clickhouse-io/` | ClickHouse DB 패턴 |
| `coding-standards/` | TypeScript/JS 코딩 표준 |
| `continuous-learning/` | 세션에서 패턴 자동 추출 |
| `frontend-patterns/` | React, Next.js 패턴 |
| `project-guidelines/` | 프로젝트별 가이드라인 템플릿 |
| `security-review/` | 보안 리뷰 체크리스트 |
| `strategic-compact/` | 전략적 컴팩트 제안 |
| `tdd-workflow/` | TDD 상세 가이드 |

---

## 📤 스킬 파일 형식

모든 스킬은 **폴더 구조**를 따릅니다:

```
skill-folder/
├── SKILL.md      # 필수: 메인 스킬 파일 (YAML frontmatter 포함)
├── scripts/      # 선택: 자동화 스크립트
└── config.json   # 선택: 설정 파일
```

**SKILL.md 형식:**
```markdown
---
name: skill-name
description: 이 스킬이 활성화되는 상황
---

# 스킬 제목

[스킬 내용]
```

---

## 🔧 스킬 경로

### 글로벌 스킬 (모든 프로젝트에 적용)

```bash
# 경로 버그 수정 (심볼릭 링크)
ln -s ~/.gemini/antigravity/skills ~/.gemini/antigravity/global_skills

# 스킬 복사
cp -r ~/dotfiles-for-antigravity/.agent/skills/* ~/.gemini/antigravity/skills/
```

### 프로젝트 스킬 (특정 프로젝트에만 적용)

```bash
# 프로젝트 루트에 복사
mkdir -p .agent
cp -R ~/dotfiles-for-antigravity/.agent/skills/. .agent/skills/
```

---

## 💡 dotfiles 구조

```
dotfiles-for-antigravity/
├── .agent/
│   ├── workflows/           # 워크플로우 (21개)
│   └── skills/              # 스킬 (9개)
│       ├── backend-patterns/
│       │   └── SKILL.md
│       ├── clickhouse-io/
│       │   └── SKILL.md
│       ├── coding-standards/
│       │   └── SKILL.md
│       ├── continuous-learning/
│       │   ├── SKILL.md
│       │   ├── config.json
│       │   └── evaluate-session.sh
│       ├── frontend-patterns/
│       │   └── SKILL.md
│       ├── project-guidelines/
│       │   └── SKILL.md
│       ├── security-review/
│       │   └── SKILL.md
│       ├── strategic-compact/
│       │   ├── SKILL.md
│       │   └── suggest-compact.sh
│       └── tdd-workflow/
│           └── SKILL.md
```

---

## 🚀 Quick Setup

```bash
# 새 프로젝트에 workflows + skills 복사
cp -R ~/dotfiles-for-antigravity/.agent/. .agent/

# 또는 선택적 복사
mkdir -p .agent
cp -R ~/dotfiles-for-antigravity/.agent/skills/. .agent/skills/
```

---

## ✅ 확인 방법

스킬이 제대로 로드되면 관련 작업 시 자동 활성화됩니다.

```
"사용 가능한 스킬 목록이 뭐야?"
```

예상 결과: 9개 스킬 모두 표시
