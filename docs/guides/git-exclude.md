# /git-exclude 가이드

> 로컬 전용 Git ignore를 설정하는 워크플로우

---

## 📌 언제 사용하나요?

`.gitignore`를 수정하지 않고 **로컬에서만** 파일 무시:
- 개인 IDE 설정
- 로컬 테스트 파일
- 임시 디버깅 파일
- 개인 설정 파일

---

## 📤 .gitignore vs git exclude

| 항목 | `.git/info/exclude` | `.gitignore` |
|------|---------------------|--------------|
| 범위 | 로컬 전용 | 팀 공유 |
| 커밋됨 | No | Yes |
| 용도 | 개인 설정 | 프로젝트 공통 |

---

## 💡 사용법

```bash
# 현재 exclude 확인
cat .git/info/exclude

# 패턴 추가
echo "my-local-file.txt" >> .git/info/exclude
echo "*.local" >> .git/info/exclude
echo "my-local-dir/" >> .git/info/exclude

# 확인
git status --ignored
```

---

## 📤 패턴 문법

| 패턴 | 의미 |
|------|------|
| `filename` | 특정 파일 |
| `*.ext` | 해당 확장자 전체 |
| `dirname/` | 디렉토리 |
| `!important.txt` | 제외 (무시 X) |
| `**/temp` | 모든 하위의 temp |

---

## ✅ 베스트 프랙티스

- ✅ 개인/머신 특정 ignore만 사용
- ✅ 왜 exclude하는지 주석
- ❌ 팀 공유 필요하면 `.gitignore` 사용
