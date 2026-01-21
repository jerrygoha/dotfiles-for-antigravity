# /e2e 가이드

> Playwright로 사용자 관점의 E2E 테스트를 생성하는 워크플로우

---

## 📌 언제 사용하나요?

| 상황 | 예시 |
|------|------|
| 중요 사용자 플로우 | "로그인→결제 플로우" |
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

## 📤 결과물

### Page Object Model

```typescript
// tests/pages/LoginPage.ts
export class LoginPage {
  async login(email: string, password: string) {
    await this.page.fill('[data-testid="email"]', email);
    await this.page.fill('[data-testid="password"]', password);
    await this.page.click('[data-testid="login-btn"]');
  }
}
```

---

## 💡 Quick Commands

```bash
npx playwright test                          # 전체 실행
npx playwright test --headed                 # 브라우저 보이게
npx playwright test --debug                  # 디버그 모드
npx playwright show-report                   # 리포트 보기
```

---

## ✅ 베스트 프랙티스

- ✅ Page Object Model 사용
- ✅ `data-testid` 속성 사용
- ✅ 핵심 플로우만 테스트
- ❌ CSS 클래스로 선택 금지
- ❌ 모든 케이스 E2E로 금지
