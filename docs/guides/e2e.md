# /e2e 완벽 상세 가이드

> Playwright로 사용자 관점의 E2E 테스트를 생성하는 워크플로우

---

## 📌 개요 및 목적

`/e2e`는 **실제 사용자 여정**을 Playwright로 테스트하는 워크플로우입니다.

**테스트 범위:**
- 로그인/회원가입 플로우
- 결제 프로세스
- 핵심 사용자 경로
- 다중 브라우저 호환성

---

## 🎯 언제 사용하나요?

### ✅ 이럴 때 사용하세요

| 상황 | 예시 |
|------|------|
| 중요 사용자 플로우 | "로그인→결제 플로우 테스트" |
| 배포 전 검증 | "핵심 기능 전체 테스트" |
| UI 상호작용 | "모달, 드롭다운 동작" |
| 다중 브라우저 | "Chrome, Firefox 호환" |

### Unit/Integration과의 차이

| Unit | Integration | E2E |
|------|------------|-----|
| 함수 단위 | API/DB 연동 | 전체 플로우 |
| 빠름 | 중간 | 느림 |
| 많이 | 적당히 | 핵심만 |

---

## 📤 기대 결과물

### Page Object Model

```typescript
// tests/pages/LoginPage.ts
export class LoginPage {
  constructor(private page: Page) {}
  
  async goto() {
    await this.page.goto('/login');
  }
  
  async login(email: string, password: string) {
    await this.page.fill('[data-testid="email"]', email);
    await this.page.fill('[data-testid="password"]', password);
    await this.page.click('[data-testid="login-btn"]');
  }
}
```

### 테스트 파일

```typescript
// tests/e2e/login-flow.spec.ts
test('user can login and view dashboard', async ({ page }) => {
  const loginPage = new LoginPage(page);
  await loginPage.goto();
  await loginPage.login('user@test.com', 'password');
  
  await expect(page.locator('h1')).toContainText('Dashboard');
});
```

### 실행 결과

```
PASS tests/e2e/login-flow.spec.ts
  ✓ user can login and view dashboard (3.2s)
  ✓ invalid login shows error (1.5s)

Artifacts:
📸 Screenshots: 2
📹 Videos: 0 (only on failure)
📊 HTML Report: playwright-report/
```

---

## 📖 상세 사용법

### Step 1: 호출

```
/e2e 로그인 후 프로필 수정하는 플로우 테스트 만들어줘
```

### Step 2: 시나리오 확인

에이전트가 테스트 시나리오를 제안:
1. 로그인 페이지 이동
2. 로그인 수행
3. 프로필 페이지 이동
4. 정보 수정
5. 저장 확인

### Step 3: 코드 생성

Page Object + 테스트 파일 생성

### Step 4: 실행

```bash
npx playwright test tests/e2e/profile.spec.ts
```

### Step 5: 결과 확인

```bash
npx playwright show-report
```

---

## ⚠️ 이런 상황엔 다른 워크플로우를!

| 상황 | 대신 사용할 워크플로우 |
|------|----------------------|
| 함수 단위 테스트 | `/tdd` |
| API 테스트 | `/testing` (integration) |
| 버그 수정 | `/debug` |
| 테스트 커버리지 | `/test-coverage` |

---

## 🔗 함께 사용하면 좋은 워크플로우

```
/write-plan          # 기능 계획
    ↓
/tdd                 # 유닛 테스트
    ↓
/testing             # 통합 테스트
    ↓
/e2e                 # E2E 테스트
    ↓
/code-review         # 코드 리뷰
```

---

## ✅ E2E 베스트 프랙티스

**DO:**
- ✅ Page Object Model 사용
- ✅ `data-testid` 속성 사용
- ✅ API 응답 대기 (timeout X)
- ✅ 핵심 플로우만 테스트
- ✅ 실패 시 artifacts 확인

**DON'T:**
- ❌ CSS 클래스로 선택
- ❌ 프로덕션에서 실행
- ❌ 모든 케이스 E2E로
- ❌ Flaky 테스트 방치

---

## 💡 Quick Commands

```bash
# 전체 E2E 실행
npx playwright test

# 특정 파일
npx playwright test tests/e2e/login.spec.ts

# 브라우저 보이게
npx playwright test --headed

# 디버그 모드
npx playwright test --debug

# 리포트 보기
npx playwright show-report
```
