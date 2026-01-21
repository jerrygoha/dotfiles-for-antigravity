# /update-docs 완벽 상세 가이드

> 소스 코드 기반으로 문서를 자동 생성/업데이트하는 워크플로우

---

## 📌 개요 및 목적

`/update-docs`는 `package.json`, `.env.example` 등 **소스 파일을 기반으로 문서를 자동 생성**하는 워크플로우입니다.

---

## 🎯 언제 사용하나요?

### ✅ 이럴 때 사용하세요

| 상황 | 예시 |
|------|------|
| 스크립트 변경 후 | "npm scripts 업데이트됨" |
| 환경변수 추가 후 | "새 API 키 추가" |
| 온보딩 문서 필요 | "새 개발자 합류" |
| 배포 문서 필요 | "운영 매뉴얼 작성" |

---

## 📤 기대 결과물

### docs/CONTRIB.md

```markdown
## Available Scripts

| Command | Description |
|---------|-------------|
| `npm run dev` | 개발 서버 실행 |
| `npm run build` | 프로덕션 빌드 |
| `npm test` | 테스트 실행 |

## Environment Variables

| Variable | Required | Description |
|----------|----------|-------------|
| DATABASE_URL | ✅ | PostgreSQL 연결 문자열 |
| API_KEY | ✅ | 외부 API 키 |
| DEBUG | ❌ | 디버그 모드 |
```

### docs/RUNBOOK.md (운영 매뉴얼)

---

## 📖 상세 사용법

### Step 1: 호출

```
/update-docs
```

### Step 2: 생성된 문서 확인

### Step 3: 수정 요청 (필요시)

```
"DATABASE_URL 설명을 더 자세히 해줘"
```

---

## ⚠️ 이런 상황엔 다른 워크플로우를!

| 상황 | 대신 사용할 워크플로우 |
|------|----------------------|
| 코드맵/아키텍처 문서 | `/update-codemaps` |
| API 문서 | 별도 API 문서 도구 |
| README 작성 | 직접 작성 |

---

## 🔗 함께 사용하면 좋은 워크플로우

```
기능 개발 완료
    ↓
/update-docs         # 문서 업데이트
    ↓
/update-codemaps     # 아키텍처 문서
    ↓
/create-pr           # PR 생성
```

---

## 💡 프로 팁

1. **Single Source of Truth**: package.json, .env.example 기준
2. **정기 업데이트**: 릴리스마다 실행
3. **오래된 문서 경고**: 90일+ 경과 시 검토 표시
