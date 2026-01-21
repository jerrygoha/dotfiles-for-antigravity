# /update-docs 가이드

> 소스 코드 기반으로 문서를 자동 생성/업데이트하는 워크플로우

---

## 📌 언제 사용하나요?

- npm scripts 변경 후
- 환경변수 추가 후
- 새 개발자 온보딩
- 릴리스 문서 업데이트

---

## 📤 생성되는 문서

### CONTRIBUTING.md

```markdown
## Prerequisites
- Node.js >= [버전]

## Setup
git clone → npm install → cp .env.example .env.local

## Available Scripts
| Command | Description |
|---------|-------------|
| npm run dev | 개발 서버 |
| npm run build | 프로덕션 빌드 |
| npm test | 테스트 실행 |

## Environment Variables
| Variable | Required | Description |
|----------|----------|-------------|
| DATABASE_URL | ✅ | DB 연결 문자열 |
| API_KEY | ✅ | 외부 API 키 |
```

---

## ✅ 베스트 프랙티스

- ✅ Single source of truth (package.json, .env.example 기준)
- ✅ 코드 변경과 함께 문서 업데이트
- ✅ 필수 환경변수 모두 포함
- ❌ 정보 중복 금지
- ❌ 문서에 시크릿 포함 금지

---

## 🔗 관련 워크플로우

- `/update-codemaps` - 아키텍처 문서
- `/create-pr` - PR에 문서 포함
