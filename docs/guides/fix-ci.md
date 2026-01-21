# /fix-ci 완벽 상세 가이드

> CI/CD 파이프라인 실패를 진단하고 해결하는 워크플로우

---

## 📌 개요 및 목적

`/fix-ci`는 GitHub Actions나 다른 CI/CD 파이프라인의 **빌드 실패를 로컬에서 재현**하고 해결하는 워크플로우입니다.

---

## 🎯 언제 사용하나요?

### ✅ 이럴 때 사용하세요

| 상황 | 예시 |
|------|------|
| CI 빌드 실패 | "GitHub Actions 실패" |
| 로컬은 되는데 CI는 안 됨 | "내 컴퓨터에선 돼요" |
| 테스트 Flaky | "가끔 실패해요" |
| 환경 차이 의심 | "CI에서만 에러" |

---

## 📤 기대 결과물

```markdown
## CI Fix Report

### Issue
GitHub Actions: test job failed

### Root Cause
환경 변수 DATABASE_URL 누락

### Fix Applied
- `.github/workflows/test.yml`: DATABASE_URL 추가
- `jest.config.js`: test 환경 설정 추가

### Verification
Local CI simulation: ✅ PASS
```

---

## 📖 상세 사용법

### Step 1: 실패 확인

```
/fix-ci
```

또는

```
/fix-ci GitHub Actions 빌드가 실패했어. 로그 봐줄래?
```

### Step 2: 로컬 재현

```bash
# CI 환경과 동일하게
rm -rf node_modules
npm ci
npm run lint
npm test
npm run build
```

### Step 3: 환경 비교

```bash
echo "Node: $(node -v)"
echo "npm: $(npm -v)"
cat .nvmrc
```

### Step 4: 문제 해결

### Step 5: 재검증 및 푸시

```bash
npm run lint && npm test && npm run build
git push
gh run watch
```

---

## ⚠️ 이런 상황엔 다른 워크플로우를!

| 상황 | 대신 사용할 워크플로우 |
|------|----------------------|
| 런타임 버그 | `/debug` |
| 테스트 로직 문제 | `/tdd` 또는 `/testing` |
| 타입 에러만 | `/fix-ci`와 유사하지만 `tsc` 집중 |

---

## 🔗 함께 사용하면 좋은 워크플로우

```
/fix-ci              # CI 문제 해결
    ↓
/testing             # 테스트 보강
    ↓
/code-review         # 수정 검토
    ↓
/create-pr           # PR 생성
```

---

## ✅ 공통 실패 원인

| 카테고리 | 원인 | 해결 |
|----------|------|------|
| Build | 의존성 누락 | `package-lock.json` 확인 |
| Lint | 스타일 위반 | `npm run lint --fix` |
| Test | 비동기 이슈 | timeout, 순서 의존성 확인 |
| Deploy | 시크릿 누락 | GitHub Secrets 확인 |
| Timeout | 느린 테스트 | 최적화 또는 limit 조정 |

---

## 💡 프로 팁

1. **로컬 재현 우선**: CI에서만 안 되면 환경 차이
2. **캐시 의심**: `rm -rf node_modules && npm ci`
3. **환경변수 체크**: `.env.example` vs CI secrets
4. **Node 버전**: `.nvmrc`와 CI 설정 일치 확인
