# /create-pr 가이드

> 잘 구조화된 Pull Request를 생성하는 워크플로우

---

## 📌 전제조건

- 변경사항이 feature 브랜치에 커밋됨
- 로컬에서 테스트 통과
- 브랜치가 타겟과 동기화됨

---

## 📤 PR 설명 템플릿

```markdown
## Summary
[이 PR이 하는 일 요약]

## Changes
- 변경사항 1
- 변경사항 2

## Type
- [ ] Bug fix
- [ ] Feature
- [ ] Breaking change
- [ ] Documentation

## Testing
- [ ] Unit tests pass
- [ ] Integration tests pass
- [ ] Manual testing

## Related Issues
Closes #[이슈번호]
```

---

## 📤 PR 제목 컨벤션

**형식**: `<type>(<scope>): <description>`

| Type | 용도 |
|------|------|
| `feat` | 새 기능 |
| `fix` | 버그 수정 |
| `docs` | 문서 |
| `refactor` | 리팩토링 |
| `test` | 테스트 추가 |

**예시:**
- `feat(auth): add OAuth2 login support`
- `fix(api): handle null response correctly`

---

## ✅ 좋은 PR 체크리스트

- [ ] 작은 크기 (< 400줄 권장)
- [ ] 하나의 관심사만
- [ ] 명확한 제목
- [ ] UI 변경 시 스크린샷
- [ ] 관련 이슈 링크

---

## 🔗 권장 흐름

```
/code-review → /testing → /create-pr
```
