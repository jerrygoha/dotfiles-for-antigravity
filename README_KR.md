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

### Step 1: 레포지토리 클론

```bash
git clone https://github.com/YOUR_USERNAME/dotfiles-for-antigravity.git
cd dotfiles-for-antigravity
```

### Step 2: 사용자 규칙 설정 (최초 1회, 전역 설정)

사용자 규칙은 모든 Antigravity 대화에 **전역**으로 적용됩니다.

1. Antigravity 설정 열기
2. "User Rules" 또는 "Custom Instructions" 섹션으로 이동
3. 원하는 템플릿의 내용을 복사하여 붙여넣기:

```bash
# 사용할 템플릿 내용 확인
cat user-rules/default.md           # 기본 전문가
cat user-rules/dev-master.md        # 고급 이중 언어 (한/영)
cat user-rules/examples/korean-dev.md    # 한국어 개발자용
```

4. 설정 저장

---

## 📦 새 프로젝트에서 Dotfiles 사용하기

### 방법 1: 프로젝트에 워크플로우 복사 (권장)

새 프로젝트마다 워크플로우 디렉토리를 복사합니다:

```bash
# 프로젝트 디렉토리로 이동
cd /path/to/your/project

# .agent 디렉토리 생성 및 워크플로우 복사
mkdir -p .agent
cp -r /path/to/dotfiles-for-antigravity/.agent/workflows .agent/

# 설정 확인
ls .agent/workflows/
```

프로젝트 구조:

```
your-project/
├── .agent/
│   └── workflows/
│       ├── brainstorm.md
│       ├── code-review.md
│       ├── debug.md
│       └── ... (14개 워크플로우 파일)
├── src/
├── package.json
└── ...
```

### 방법 2: 심볼릭 링크 (개발용)

dotfiles 수정 시 자동 업데이트를 원할 경우:

```bash
cd /path/to/your/project
mkdir -p .agent
ln -s /path/to/dotfiles-for-antigravity/.agent/workflows .agent/workflows
```

### 방법 3: Git 서브모듈

팀 프로젝트에서 모두가 같은 워크플로우를 사용해야 할 경우:

```bash
cd /path/to/your/project
git submodule add https://github.com/YOUR_USERNAME/dotfiles-for-antigravity.git .dotfiles
mkdir -p .agent
cp -r .dotfiles/.agent/workflows .agent/
```

---

## 🎯 워크플로우 사용법

프로젝트에 워크플로우가 설정되면 슬래시 명령어로 사용합니다:

```
/brainstorm       # 대화형 설계 개선 시작
/debug            # 근본 원인 분석으로 체계적 디버깅
/write-plan       # 코딩 전 구현 계획 작성
/execute-plan     # 체크포인트와 함께 계획 실행
/code-review      # 보안 및 품질 체크리스트 실행
/create-pr        # 구조화된 PR 생성
/handoff          # 나중을 위해 세션 컨텍스트 저장
/pickup           # 이전 핸드오프에서 재개
```

### 워크플로우 사용 예시

```
User: /debug

Antigravity: 체계적 디버깅 프로세스를 시작합니다...

## Phase 1: 재현 및 관찰
어떤 문제가 발생하고 있나요? 다음 정보를 제공해 주세요:
1. 예상 동작
2. 실제 동작
3. 에러 메시지 (있는 경우)
...
```

---

## 🔧 프로젝트별 커스터마이징

### 프로젝트 컨텍스트 추가

프로젝트 루트에 `ANTIGRAVITY.md` 파일 생성:

```bash
# 템플릿 복사
cp /path/to/dotfiles-for-antigravity/ANTIGRAVITY.md /path/to/your/project/
```

프로젝트 정보로 커스터마이즈:

```markdown
# ANTIGRAVITY.md

## 프로젝트 개요
[프로젝트 설명]

## 기술 스택
- Framework: Next.js 14
- Database: PostgreSQL
- Styling: Tailwind CSS

## 주요 명령어
npm run dev    # 개발 서버 시작
npm run test   # 테스트 실행
npm run build  # 프로덕션 빌드

## 아키텍처 노트
[프로젝트별 참고사항]
```

### 프로젝트용 커스텀 워크플로우 만들기

프로젝트별 워크플로우가 필요한 경우:

```bash
# 커스텀 워크플로우 생성
touch .agent/workflows/deploy-staging.md
```

---

## � 설정 레퍼런스

### 사용자 규칙 템플릿

| 템플릿 | 적합한 대상 |
|--------|------------|
| `default.md` | 일반 개발, 깔끔한 코드 중심 |
| `dev-master.md` | 한국 개발자, 이중 언어 프로젝트 |
| `examples/frontend-dev.md` | React, Next.js, Vue 프로젝트 |
| `examples/backend-dev.md` | Node.js, Python API, 마이크로서비스 |
| `examples/devops-engineer.md` | 인프라, CI/CD, Kubernetes |
| `examples/python-dev.md` | Python 백엔드, 데이터 사이언스, ML |
| `examples/korean-dev.md` | 한국 개발자, 로컬라이즈 프로젝트 |
| `examples/minimal.md` | 빠른 작업, 코드 중심 응답 |

### 워크플로우 명령어

| 명령어 | 사용 시점 |
|--------|----------|
| `/brainstorm` | 창의적 솔루션이나 설계 아이디어 필요 시 |
| `/write-plan` | 복잡한 기능 시작 전 |
| `/execute-plan` | 승인된 계획을 체계적으로 실행 |
| `/debug` | 원인 불명의 버그 해결 |
| `/code-review` | 코드 병합 전, 보안 감사 |
| `/testing` | 단위/통합 테스트 작성 |
| `/create-pr` | PR 열 준비 완료 |
| `/fix-ci` | CI 파이프라인 실패 시 |
| `/git-workflow` | Git 작업, 브랜칭 전략 |
| `/research` | 기술 비교 필요 시 |
| `/handoff` | 세션 종료, 컨텍스트 저장 |
| `/pickup` | 이전 세션 재개 |

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
