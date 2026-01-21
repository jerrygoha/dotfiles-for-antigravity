# /create-pr 완벽 상세 가이드

> 잘 구조화된 Pull Request를 생성하는 워크플로우

---

## 📌 개요 및 목적

`/create-pr`은 **리뷰하기 좋은 PR**을 체계적으로 생성하는 워크플로우입니다.

---

## 🎯 언제 사용하나요?

### ✅ 이럴 때 사용하세요

| 상황 | 조건 |
|------|------|
| 기능 구현 완료 | 테스트 통과, 리뷰 완료 |
| 코드 리뷰 완료 | `/code-review` PASS |
| 커밋 정리 완료 | 의미 있는 커밋 단위 |

---

## 📤 기대 결과물

### PR 설명 템플릿

```markdown
## Summary
OAuth 기반 Google 로그인 기능 추가

## Changes
- NextAuth.js 설정 추가
- Google Provider 연동
- 콜백 처리 로직 구현
- 로그인 UI 컴포넌트 추가

## Type
- [x] Feature
- [ ] Bug fix
- [ ] Breaking change
- [ ] Docs

## Testing
- [x] Unit tests (auth.test.ts)
- [x] Integration tests (callback.test.ts)
- [x] Manual testing (로컬 환경)

## Screenshots
[로그인 화면 스크린샷]

## Related
Closes #123

## Checklist
- [x] 스타일 가이드 준수
- [x] 셀프 리뷰 완료
- [x] 문서 업데이트
```

---

## 📖 상세 사용법

### Step 1: 사전 준비

```bash
# 브랜치 확인
git fetch origin && git rebase origin/main

# 변경 확인
git log origin/main..HEAD --oneline
```

### Step 2: 호출

```
/create-pr
```

### Step 3: PR 설명 확인

에이전트가 PR 설명을 생성합니다.

### Step 4: PR 생성

```bash
gh pr create
```

### Step 5: 리뷰어 추가

```bash
gh pr edit --add-reviewer @username
gh pr edit --add-label "enhancement"
```

---

## ⚠️ 이런 상황엔 다른 워크플로우를!

| 상황 | 대신 사용할 워크플로우 |
|------|----------------------|
| 코드 리뷰 안 함 | `/code-review` 먼저 |
| 테스트 실패 | `/testing` 또는 `/debug` |
| 빌드 실패 | `/fix-ci` |

---

## 🔗 함께 사용하면 좋은 워크플로우

```
/code-review         # 품질 검토
    ↓
/testing             # 테스트 확인
    ↓
/create-pr           # PR 생성
```

---

## ✅ 좋은 PR 체크리스트

- [ ] 하나의 관심사만 (기능 OR 리팩토링)
- [ ] 작은 크기 (200-400 lines 권장)
- [ ] 명확한 제목
- [ ] UI 변경 시 스크린샷 포함
- [ ] 테스트 추가됨

---

## 💡 프로 팁

1. **작은 PR**: 리뷰어 부담 줄이기
2. **제목 컨벤션**: `feat:`, `fix:`, `refactor:` 등
3. **Draft PR**: 진행 중이면 Draft로 생성
4. **셀프 리뷰**: PR 생성 후 본인이 먼저 리뷰
