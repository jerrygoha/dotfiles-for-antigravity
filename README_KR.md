# Antigravity를 위한 Dotfiles

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

> **[Antigravity](https://gemini.google.com/)를 위한 전문 dotfiles 시스템** - Google의 AI 기반 에이전트 코딩 어시스턴트

🇺🇸 [English Documentation](./README.md)

---

## ✨ 주요 기능

- **14개 워크플로우 정의** - 개발 자동화를 위한 종합적인 `.agent/workflows/`
- **8개 사용자 규칙 템플릿** - 다양한 개발 스타일에 맞춘 사전 구성 프롬프트
- **글로벌 메모리 템플릿** - 프로젝트 간 일관된 컨텍스트 설정
- **이중 언어 문서** - 영어 & 한국어 문서 제공

---

## 🚀 빠른 시작

### 1. 레포지토리 클론

```bash
git clone https://github.com/YOUR_USERNAME/dotfiles-for-antigravity.git
cd dotfiles-for-antigravity
```

### 2. 사용자 규칙 설정

```bash
# 옵션 1: 기본 템플릿 사용
cat user-rules/default.md

# 옵션 2: 고급 Dev-Master 템플릿 (한/영 이중 언어)
cat user-rules/dev-master.md

# 옵션 3: 특정 페르소나 선택
cat user-rules/examples/korean-dev.md
```

내용을 복사하여 Antigravity 사용자 설정에 붙여넣습니다.

### 3. 워크플로우 설정

```bash
cp -r .agent/workflows/ /path/to/your/project/.agent/workflows/
```

---

## 📁 디렉토리 구조

```
dotfiles-for-antigravity/
├── README.md               # 영어 문서
├── README_KR.md            # 한국어 문서 (현재)
├── ANTIGRAVITY.md          # 에이전트 컨텍스트 파일
├── .agent/
│   └── workflows/          # 14개 워크플로우 정의
│       ├── brainstorm.md, code-review.md, create-pr.md
│       ├── debug.md, execute-plan.md, fix-ci.md
│       ├── git-exclude.md, git-workflow.md, handoff.md
│       ├── pickup.md, research.md, testing.md
│       └── write-plan.md, create-workflow.md
├── user-rules/
│   ├── default.md          # 기본 사용자 규칙
│   ├── dev-master.md       # 고급 이중 언어 프롬프트
│   └── examples/           # 6개 페르소나 예제
└── memory-templates/
    └── global-memory.md
```

---

## 🔧 설정 파일

### 사용자 규칙 템플릿

| 템플릿 | 설명 |
|--------|------|
| `default.md` | 깔끔하고 전문적인 코드를 위한 기본 규칙 |
| `dev-master.md` | C.O.D.E.R. 프레임워크 포함 고급 이중 언어 |
| `examples/frontend-dev.md` | React/Next.js 중심 |
| `examples/backend-dev.md` | API 및 서비스 중심 |
| `examples/devops-engineer.md` | 인프라 및 신뢰성 |
| `examples/python-dev.md` | Python 모범 사례 |
| `examples/korean-dev.md` | 한국어 개발자 이중 언어 설정 |
| `examples/minimal.md` | 간결한 코드 중심 응답 |

### 워크플로우

| 워크플로우 | 설명 |
|------------|------|
| `/brainstorm` | 소크라테스식 대화를 통한 설계 개선 |
| `/code-review` | 보안 감사, 성능 리뷰 체크리스트 |
| `/create-pr` | 구조화된 PR 생성 |
| `/debug` | 4단계 근본 원인 분석 |
| `/execute-plan` | 체크포인트와 함께 계획 실행 |
| `/fix-ci` | CI/CD 실패 진단 및 수정 |
| `/git-workflow` | Git 브랜칭, 커밋, PR |
| `/handoff` | 세션 연속성을 위한 핸드오프 문서 생성 |
| `/pickup` | 이전 핸드오프에서 작업 재개 |
| `/research` | 인용과 함께 웹 리서치 |
| `/testing` | 단위/통합 테스트 가이드라인 |
| `/write-plan` | 상세 구현 계획 작성 |

---

## 🤝 기여하기

기여를 환영합니다! [CONTRIBUTING.md](./CONTRIBUTING.md)를 참조하세요.

---

## 📄 라이선스

MIT 라이선스 - [LICENSE](./LICENSE) 참조

---

## 🙏 감사의 말

- [baleen37/dotfiles](https://github.com/baleen37/dotfiles) (Claude Code dotfiles)에서 영감
- [Antigravity](https://gemini.google.com/) 커뮤니티를 위해 제작
