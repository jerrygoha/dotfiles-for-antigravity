# /git-workflow 가이드

> 브랜치, 커밋, PR 관리를 위한 Git 워크플로우

---

## 📤 브랜치 네이밍

| Type | 형식 | 예시 |
|------|------|------|
| Feature | `feat/설명` | `feat/user-auth` |
| Bug fix | `fix/설명` | `fix/login-error` |
| Refactor | `refactor/설명` | `refactor/api-layer` |
| Docs | `docs/설명` | `docs/readme-update` |
| Test | `test/설명` | `test/add-unit-tests` |

---

## 📤 커밋 메시지 컨벤션

**형식**: `<type>(<scope>): <description>`

```
feat(auth): add OAuth2 login support
fix(api): handle null response correctly
docs: update README with setup steps
refactor(db): optimize query performance
```

**규칙:**
- 명령형 사용 ("add" not "added")
- 첫 줄 72자 미만
- 이슈 참조: `Closes #123`

---

## 📤 Merge 전략

| 전략 | 언제 사용 |
|------|----------|
| Squash merge | Feature 브랜치 (깔끔한 히스토리) |
| Rebase merge | 장기 실행 브랜치 |
| Merge commit | 릴리스 브랜치 |

**Merge 후:** 브랜치 삭제

---

## 🔗 관련 워크플로우

- `/create-pr` - PR 생성
- `/code-review` - 커밋 전 리뷰
