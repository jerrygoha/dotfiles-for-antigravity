# Filtered Features (Claude Code Specific)

이 문서는 **everything-claude-code** 레포지토리에서 Antigravity와 호환되지 않아 필터링된 기능들을 기록합니다.

> ⚠️ 이 기능들은 Claude Code 전용이며 Antigravity에서는 지원되지 않습니다.

---

## 1. Hooks System

### 경로
`.reference/everything-claude-code/hooks/`

### 파일 목록
- `hooks.json` - PreToolUse, PostToolUse, Stop 훅 정의
- `memory-persistence/` - 세션 간 메모리 유지
- `strategic-compact/` - 전략적 컨텍스트 압축

### 기능 설명

#### PreToolUse Hooks
도구 사용 전 실행되는 자동화:
- dev 서버가 tmux 외부에서 실행되면 블록
- console.log 발견 시 경고
- 불필요한 .md 파일 생성 블록

#### PostToolUse Hooks
도구 사용 후 실행되는 자동화:
- PR 생성 후 URL 로깅
- TypeScript 파일 편집 후 자동 포맷팅
- TypeScript 타입 체크

#### Stop Hooks
세션 종료 시 실행:
- console.log 최종 감사
- 세션 상태 저장
- 패턴 평가

### 대안
Antigravity에서는:
- 워크플로우에 수동 체크 단계 포함
- `/code-review` 워크플로우로 console.log 체크
- `/handoff` 워크플로우로 세션 상태 저장

---

## 2. MCP (Model Context Protocol) Configs

### 경로
`.reference/everything-claude-code/mcp-configs/`

### 파일
- `mcp-servers.json` - GitHub, Supabase, Vercel, Railway 등 MCP 서버 설정

### 기능 설명
MCP 서버를 통해 외부 서비스와 직접 통합:
- GitHub PR/Issue 관리
- Supabase 데이터베이스 조회
- Vercel 배포 관리
- Railway 서비스 관리

### 대안
Antigravity에서는:
- 직접 CLI 명령어 사용 (`gh`, `vercel`, `railway`)
- API 호출 스크립트 작성
- 워크플로우에 명령어 포함

---

## 3. Memory Persistence System

### 경로
`.reference/everything-claude-code/hooks/memory-persistence/`

### 스크립트
- `pre-compact.sh` - 압축 전 상태 저장
- `session-start.sh` - 세션 시작 시 이전 컨텍스트 로드
- `session-end.sh` - 세션 종료 시 상태 저장

### 기능 설명
세션 간 컨텍스트 자동 유지:
- 자동 상태 저장/복원
- 압축 전 중요 정보 보존

### 대안
Antigravity에서는:
- `/handoff` 워크플로우로 수동 상태 저장
- `/pickup` 워크플로우로 수동 복원
- `session-management.md` 규칙 참고

---

## 4. Strategic Compact System

### 경로
`.reference/everything-claude-code/hooks/strategic-compact/`

### 스크립트
- `suggest-compact.sh` - 논리적 단계 전환 시 압축 제안

### 기능 설명
50회 도구 호출 후 `/compact` 제안:
- 탐색 → 구현 전환 시
- 마일스톤 완료 후
- 컨텍스트가 오래된 경우

### 대안
Antigravity에서는:
- `session-management.md` 규칙의 100K 토큰 기준 참고
- 2-3시간마다 `/handoff` 수동 실행

---

## 5. Plugins Ecosystem

### 경로
`.reference/everything-claude-code/plugins/`

### 파일
- `README.md` - 플러그인, 마켓플레이스, 스킬 가이드

### 기능 설명
Claude Code 플러그인 생태계:
- 커뮤니티 스킬 공유
- 마켓플레이스 통합

### 대안
Antigravity에서는:
- `user-rules/skills/` 디렉토리에 직접 스킬 추가
- `.agent/workflows/` 디렉토리에 워크플로우 추가

---

## 6. Statusline Config

### 경로
`.reference/everything-claude-code/examples/statusline.json`

### 기능 설명
Claude Code 상태 표시줄 커스터마이징

### 대안
Antigravity 자체 UI 사용

---

## 7. Sessions Directory

### 경로
`.reference/everything-claude-code/examples/sessions/`

### 기능 설명
Claude Code 세션 관리 예시

### 대안
Antigravity에서는:
- `.agent/handoffs/` 디렉토리 사용
- `/handoff`, `/pickup` 워크플로우 활용

---

## 원본 참조

필터링된 기능의 원본은 다음 경로에서 확인 가능:
```
.reference/everything-claude-code/
├── hooks/
│   ├── hooks.json
│   ├── memory-persistence/
│   └── strategic-compact/
├── mcp-configs/
├── plugins/
└── examples/
    ├── statusline.json
    └── sessions/
```

---

## 향후 Antigravity 지원 시

이 기능들이 Antigravity에서 지원될 경우:
1. 이 문서 업데이트
2. 해당 기능 마이그레이션
3. 관련 워크플로우 추가
