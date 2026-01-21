# /git-exclude 완벽 상세 가이드

> 로컬 전용 Git ignore를 설정하는 워크플로우

---

## 📌 개요 및 목적

`/git-exclude`는 `.gitignore`를 수정하지 않고 **로컬에서만 파일을 무시**하는 워크플로우입니다.

---

## 🎯 언제 사용하나요?

### ✅ 이럴 때 사용하세요

| 상황 | 예시 |
|------|------|
| 개인 IDE 설정 | ".idea/, .vscode/" |
| 로컬 테스트 파일 | "my-test.ts" |
| 임시 디버깅 파일 | "debug.log" |
| 개인 설정 | ".env.local.bak" |

### .gitignore vs git exclude

| Aspect | `.git/info/exclude` | `.gitignore` |
|--------|---------------------|--------------|
| Scope | 로컬 전용 | 팀 공유 |
| Committed | No | Yes |
| Use case | 개인 설정 | 프로젝트 공통 |

---

## 📤 기대 결과물

```bash
# .git/info/exclude에 추가됨
my-local-notes.md
*.local
debug-files/
```

---

## 📖 상세 사용법

### Step 1: 현재 exclude 확인

```bash
cat .git/info/exclude
```

### Step 2: 패턴 추가

```
/git-exclude my-personal-notes.md 추가해줘
```

### Step 3: 확인

```bash
git status --ignored
```

---

## ⚠️ 이런 상황엔 다른 워크플로우를!

| 상황 | 대신 사용할 워크플로우 |
|------|----------------------|
| 팀 공유 ignore | `.gitignore` 직접 수정 |
| 파일 삭제 | 일반 rm 명령 |

---

## ✅ 패턴 문법

| Pattern | Meaning |
|---------|---------|
| `filename` | 특정 파일 |
| `*.ext` | 확장자 전체 |
| `dirname/` | 디렉토리 |
| `!important.txt` | 제외 (무시 X) |
| `**/temp` | 모든 하위의 temp |

---

## 💡 프로 팁

1. **개인용만**: 팀 공유 필요하면 .gitignore
2. **이유 기록**: 왜 exclude하는지 주석
3. **정기 정리**: 불필요한 패턴 제거
