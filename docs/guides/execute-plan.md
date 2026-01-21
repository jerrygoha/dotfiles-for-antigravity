# /execute-plan 완벽 상세 가이드

> 수립된 계획을 단계별로 실행하며 검증하는 워크플로우

---

## 📌 개요 및 목적

`/execute-plan`은 `/write-plan`으로 수립된 계획을 **단계별로 실행**하면서 각 Phase마다 검증하는 워크플로우입니다.

**왜 필요한가요?**
- 계획대로 체계적 실행
- Phase별 검증으로 품질 보장
- 문제 발생 시 빠른 롤백
- 진행 상황 추적 가능

---

## 🎯 언제 사용하나요?

### ✅ 이럴 때 사용하세요

| 상황 | 조건 |
|------|------|
| `/write-plan` 완료 후 | ↔ 승인된 계획이 있음 |
| Phase별 실행 필요 | ↔ 중간 검증이 중요함 |
| 롤백 가능성 있음 | ↔ 안전하게 진행해야 함 |

### 📋 구체적인 사용 시나리오

**시나리오: 결제 시스템 통합**
```
1. /write-plan으로 계획 수립 완료
2. /execute-plan 호출
3. Phase 1 (Infrastructure) 완료 → 검증
4. Phase 2 (Subscription) 완료 → 검증
5. 전체 완료
```

---

## 📤 기대 결과물

### 각 Phase 완료 시

```markdown
## Phase 1 Complete ✅

**Done:**
- Stripe SDK 설치 완료
- 환경변수 설정 완료
- 웹훅 엔드포인트 생성

**Verified:**
- Build: ✅
- Tests: ✅
- Lint: ✅

**Next:** Phase 2 - Subscription Flow
Continue? [Y/N]
```

### 전체 완료 시

```markdown
## Execution Complete ✅

### Completed Phases
- [x] Phase 1: Infrastructure
- [x] Phase 2: Subscription
- [x] Phase 3: One-time Payment

### Key Changes
- Created: 8 files
- Modified: 3 files

### Rollback Command
git revert abc123..def456

### Next Steps
1. /code-review
2. /create-pr
```

---

## 📖 상세 사용법

### Step 1: 계획 확인

```
/execute-plan
```

### Step 2: Phase별 실행

에이전트가 한 Phase씩 실행하고 확인을 요청:
```
Phase 1 완료. 계속 진행할까요?
```

### Step 3: 검증 및 진행

- **"yes"**: 다음 Phase로
- **"문제 있어, [설명]"**: 수정 후 재시도
- **"중단해"**: 현재 상태 저장

### Step 4: 롤백 (필요시)

문제 발생 시:
```
Phase 2에서 문제가 발생했어. Phase 1으로 롤백해줘.
```

---

## ⚠️ 이런 상황엔 다른 워크플로우를!

| 상황 | 대신 사용할 워크플로우 |
|------|----------------------|
| 계획이 없음 | `/write-plan` 먼저 |
| 빌드 에러 발생 | `/fix-ci` |
| 테스트 실패 | `/debug` 또는 `/tdd` |
| 아이디어 단계 | `/brainstorm` |

---

## 🔗 함께 사용하면 좋은 워크플로우

### 권장 흐름

```
/write-plan          # 계획 수립
    ↓
/execute-plan        # 단계별 실행
    ↓ (Phase 완료마다)
/testing 또는 /tdd   # 테스트 확인
    ↓
/code-review         # 품질 검토
    ↓
/create-pr           # PR 생성
```

### 장시간 작업 시

```
/execute-plan → Phase 1, 2 완료
    ↓
/handoff             # 세션 저장
    ↓
(새 세션)
    ↓
/pickup              # 복원
    ↓
/execute-plan        # Phase 3부터 계속
```

---

## ✅ 체크리스트

### 실행 전

- [ ] 승인된 계획이 있는가?
- [ ] 현재 브랜치가 올바른가?
- [ ] 로컬 변경사항 커밋됐는가?

### Phase 완료 시

- [ ] 빌드 성공하는가?
- [ ] 테스트 통과하는가?
- [ ] 예상대로 동작하는가?

### 전체 완료 시

- [ ] 모든 Goals 달성했는가?
- [ ] 롤백 방법 기록됐는가?
- [ ] 다음 단계 명확한가?

---

## 💡 프로 팁

1. **작은 커밋**: Phase 내에서도 의미 있는 단위로 커밋
2. **검증 자동화**: `npm test && npm run build` 자동 실행
3. **중간 저장**: 2-3 Phase마다 `/handoff`
4. **문서화**: 예상과 다른 결과는 기록
