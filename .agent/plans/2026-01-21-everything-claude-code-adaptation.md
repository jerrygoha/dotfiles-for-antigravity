# Everything Claude Code → Antigravity 완전 마이그레이션

## Problem Statement

[everything-claude-code](https://github.com/affaan-m/everything-claude-code) 레포지토리의 콘텐츠를 **100% 활용**하여 Antigravity 전용 dotfiles를 재구성합니다. 기존 콘텐츠는 아카이빙하고, Claude Code 전용 기능은 필터링하여 문서화합니다.

> [!IMPORTANT]
> **핵심 목표**: 이 프로젝트는 **다른 프로젝트에 바로 적용할 수 있는 에이전트 설정 파일**을 제공하는 것입니다.  
> 한 번에 복사해서 넣을 수 있는 깔끔한 구조와 상세한 사용 가이드가 필요합니다.

---

## Goals

- [x] everything-claude-code 레포지토리 클론 및 분석
- [ ] 기존 콘텐츠 아카이빙 (`_archive/` 디렉토리)
- [ ] Claude Code 전용 기능 필터링 및 문서화
- [ ] Antigravity 호환 콘텐츠 변환 및 배치
- [ ] 세션 관리 규칙 추가 (100K 토큰 권장)
- [ ] 원클릭 배포 가능한 파일 구조 생성
- [ ] 상세한 사용 가이드 작성

## Non-Goals

- Claude Code hooks/MCP 기능 직접 이식 (문서화만)
- 기존 콘텐츠 영구 삭제 (아카이빙 처리)

---

## Compatibility Analysis

### ✅ Antigravity 호환 (변환 후 사용)

| 원본 경로 | 변환 대상 | 비고 |
|----------|----------|------|
| `commands/*.md` | `.agent/workflows/*.md` | YAML frontmatter 동일 형식 |
| `rules/*.md` | `user-rules/rules/*.md` | 규칙 문서로 통합 |
| `skills/*.md` | `user-rules/skills/*.md` | 도메인 지식 정리 |
| `agents/*.md` | `user-rules/agents/*.md` | 페르소나/가이드로 변환 |
| `contexts/*.md` | `user-rules/contexts/*.md` | 컨텍스트 모드 정의 |
| `examples/CLAUDE.md` | `ANTIGRAVITY.md` | 프로젝트 컨텍스트 템플릿 |
| `examples/user-CLAUDE.md` | `user-rules/default.md` | 사용자 규칙 템플릿 |

### ❌ Antigravity 비호환 (필터링 → 문서화)

| 원본 경로 | 이유 | 문서화 위치 |
|----------|------|------------|
| `hooks/hooks.json` | Antigravity는 hooks 미지원 | `docs/FILTERED.md` |
| `hooks/memory-persistence/` | Claude 전용 메모리 시스템 | `docs/FILTERED.md` |
| `hooks/strategic-compact/` | Claude 전용 컴팩트 시스템 | `docs/FILTERED.md` |
| `mcp-configs/` | MCP 서버 설정 | `docs/FILTERED.md` |
| `plugins/` | Claude 플러그인 생태계 | `docs/FILTERED.md` |
| `examples/statusline.json` | Claude 상태 표시줄 | `docs/FILTERED.md` |
| `examples/sessions/` | Claude 세션 관리 | `docs/FILTERED.md` |

---

## Target File Structure

다른 프로젝트에 복사해서 사용할 최종 구조:

```
project-to-use/                   # 대상 프로젝트
├── .agent/
│   ├── workflows/               # 슬래시 커맨드 정의
│   │   ├── tdd.md              # /tdd - TDD 개발
│   │   ├── plan.md             # /plan - 구현 계획
│   │   ├── e2e.md              # /e2e - E2E 테스트
│   │   ├── code-review.md      # /code-review
│   │   ├── build-fix.md        # /build-fix
│   │   ├── refactor-clean.md   # /refactor-clean
│   │   ├── test-coverage.md    # /test-coverage
│   │   ├── update-docs.md      # /update-docs
│   │   ├── learn.md            # /learn - 패턴 추출
│   │   ├── handoff.md          # /handoff - 세션 인계
│   │   └── pickup.md           # /pickup - 세션 재개
│   ├── handoffs/                # 핸드오프 문서 저장
│   └── plans/                   # 구현 계획 저장
│
└── ANTIGRAVITY.md               # 프로젝트 컨텍스트 (복사해서 사용)
```

### User Rules (글로벌 설정)

```
~/.config/antigravity/           # 또는 Antigravity 설정 경로
├── user-rules/
│   ├── default.md              # 기본 사용자 규칙
│   ├── rules/                  # Always-follow 규칙
│   │   ├── security.md
│   │   ├── coding-style.md
│   │   ├── testing.md
│   │   ├── git-workflow.md
│   │   └── session-management.md  # ⭐ 100K 토큰 관리
│   ├── skills/                 # 도메인 지식
│   │   ├── coding-standards.md
│   │   ├── backend-patterns.md
│   │   └── frontend-patterns.md
│   ├── agents/                 # 페르소나 가이드
│   │   ├── planner.md
│   │   ├── architect.md
│   │   ├── code-reviewer.md
│   │   └── security-reviewer.md
│   └── contexts/               # 컨텍스트 모드
│       ├── dev.md
│       ├── review.md
│       └── research.md
```

---

## Proposed Changes

### Phase 1: 기존 콘텐츠 아카이빙 (~15min)

#### [NEW] `_archive/` 디렉토리 생성
기존 `.agent/workflows/`, `user-rules/`, `memory-templates/` 이동

---

### Phase 2: Workflows 마이그레이션 (~1.5h)

`commands/*.md` → `.agent/workflows/*.md`

#### [NEW] `.agent/workflows/tdd.md`
TDD 개발 워크플로우

#### [NEW] `.agent/workflows/plan.md`
구현 계획 수립 (기존 write-plan.md 대체)

#### [NEW] `.agent/workflows/e2e.md`
Playwright E2E 테스트

#### [NEW] `.agent/workflows/code-review.md`
코드 리뷰 체크리스트

#### [NEW] `.agent/workflows/build-fix.md`
빌드 에러 해결

#### [NEW] `.agent/workflows/refactor-clean.md`
리팩토링 및 데드 코드 정리

#### [NEW] `.agent/workflows/test-coverage.md`
테스트 커버리지 분석

#### [NEW] `.agent/workflows/update-docs.md`
문서 동기화

#### [NEW] `.agent/workflows/update-codemaps.md`
코드맵 업데이트

#### [NEW] `.agent/workflows/learn.md`
패턴 추출 및 학습

#### [KEEP] `.agent/workflows/handoff.md`
기존 핸드오프 유지 (Claude 버전과 비교 후 보완)

#### [KEEP] `.agent/workflows/pickup.md`
기존 픽업 유지

---

### Phase 3: User Rules 재구성 (~1.5h)

#### [NEW] `user-rules/default.md`
`examples/user-CLAUDE.md` 기반 기본 규칙

#### [NEW] `user-rules/rules/security.md`
보안 체크리스트

#### [NEW] `user-rules/rules/coding-style.md`
코딩 스타일 가이드

#### [NEW] `user-rules/rules/testing.md`
테스트 가이드라인

#### [NEW] `user-rules/rules/git-workflow.md`
Git 워크플로우

#### [NEW] `user-rules/rules/session-management.md`
⭐ **세션 관리 규칙** - 100K 토큰 초과 시 새 세션 권장

---

### Phase 4: Skills & Agents 마이그레이션 (~1h)

#### [NEW] `user-rules/skills/coding-standards.md`
언어별 코딩 표준

#### [NEW] `user-rules/skills/backend-patterns.md`
백엔드 패턴

#### [NEW] `user-rules/skills/frontend-patterns.md`
프론트엔드 패턴

#### [NEW] `user-rules/agents/planner.md`
플래너 에이전트 가이드

#### [NEW] `user-rules/agents/architect.md`
아키텍트 에이전트 가이드

#### [NEW] `user-rules/agents/code-reviewer.md`
코드 리뷰어 가이드

#### [NEW] `user-rules/agents/security-reviewer.md`
보안 리뷰어 가이드

---

### Phase 5: Contexts 마이그레이션 (~30min)

#### [NEW] `user-rules/contexts/dev.md`
개발 모드 컨텍스트

#### [NEW] `user-rules/contexts/review.md`
리뷰 모드 컨텍스트

#### [NEW] `user-rules/contexts/research.md`
리서치 모드 컨텍스트

---

### Phase 6: 문서화 (~1h)

#### [NEW] `docs/FILTERED.md`
⭐ **필터링된 Claude 전용 기능 문서화**
- hooks.json 전체 내용
- memory-persistence 스크립트
- strategic-compact 시스템
- MCP 서버 설정
- 플러그인 생태계 설명

#### [NEW] `docs/QUICK-START.md`
⭐ **빠른 시작 가이드**
- 프로젝트에 적용하는 방법
- 워크플로우 사용법
- 커스터마이징 방법

#### [NEW] `docs/SESSION-MANAGEMENT.md`
⭐ **세션 관리 가이드**
- 100K 토큰 기준 설명
- handoff/pickup 사용법
- 컨텍스트 최적화 팁

#### [MODIFY] `README.md`
전체 프로젝트 소개 재작성

#### [MODIFY] `ANTIGRAVITY.md`
프로젝트 템플릿 역할로 재구성

---

## Session Management Rule (100K Token)

```markdown
# Session Management Rules

## Token Threshold
- **100,000 tokens**: 새 세션 전환 권장 시점
- 현재 세션의 토큰 사용량이 100K를 초과하면:
  1. `/handoff` 명령으로 현재 상태 저장
  2. 새 세션 시작
  3. `/pickup [handoff-file]`로 컨텍스트 복원

## 권장 패턴
1. **대규모 리팩토링**: 단계별로 handoff 생성
2. **복잡한 디버깅**: 문제 해결 후 learn으로 패턴 저장
3. **장시간 개발**: 2-3시간마다 handoff 권장

## 자동 알림 (권장)
세션 시작 시 다음 메시지 표시:
> 💡 이 세션에서 100,000 토큰을 초과하면 `/handoff`로 상태를 저장하고 
> 새 세션에서 `/pickup`으로 이어서 작업하세요.
```

---

## Implementation Steps

### Phase 1: 아카이빙 (~15min)
- [ ] 1.1 `_archive/` 디렉토리 생성
- [ ] 1.2 기존 `.agent/workflows/` 이동 (handoff, pickup 제외)
- [ ] 1.3 기존 `user-rules/` 이동
- [ ] 1.4 기존 `memory-templates/` 이동

### Phase 2: Workflows (~1.5h)
- [ ] 2.1 `commands/tdd.md` 변환
- [ ] 2.2 `commands/plan.md` 변환
- [ ] 2.3 `commands/e2e.md` 변환
- [ ] 2.4 `commands/code-review.md` 변환
- [ ] 2.5 `commands/build-fix.md` 변환
- [ ] 2.6 `commands/refactor-clean.md` 변환
- [ ] 2.7 `commands/test-coverage.md` 변환
- [ ] 2.8 `commands/update-docs.md` 변환
- [ ] 2.9 `commands/update-codemaps.md` 변환
- [ ] 2.10 `commands/learn.md` 변환
- [ ] 2.11 기존 handoff.md 보완
- [ ] 2.12 기존 pickup.md 보완

### Phase 3: User Rules (~1.5h)
- [ ] 3.1 `user-rules/rules/` 디렉토리 구조 생성
- [ ] 3.2 `examples/user-CLAUDE.md` → `default.md` 변환
- [ ] 3.3 `rules/security.md` 변환
- [ ] 3.4 `rules/coding-style.md` 변환
- [ ] 3.5 `rules/testing.md` 변환
- [ ] 3.6 `rules/git-workflow.md` 변환
- [ ] 3.7 `session-management.md` 신규 작성

### Phase 4: Skills & Agents (~1h)
- [ ] 4.1 디렉토리 구조 생성
- [ ] 4.2 `skills/coding-standards.md` 핵심 추출
- [ ] 4.3 `skills/backend-patterns.md` 핵심 추출
- [ ] 4.4 `skills/frontend-patterns.md` 핵심 추출
- [ ] 4.5 `agents/planner.md` 변환
- [ ] 4.6 `agents/architect.md` 변환
- [ ] 4.7 `agents/code-reviewer.md` 변환
- [ ] 4.8 `agents/security-reviewer.md` 변환

### Phase 5: Contexts (~30min)
- [ ] 5.1 `contexts/dev.md` 변환
- [ ] 5.2 `contexts/review.md` 변환
- [ ] 5.3 `contexts/research.md` 변환

### Phase 6: 문서화 (~1h)
- [ ] 6.1 `docs/FILTERED.md` 작성 (필터링 항목 상세)
- [ ] 6.2 `docs/QUICK-START.md` 작성
- [ ] 6.3 `docs/SESSION-MANAGEMENT.md` 작성
- [ ] 6.4 `README.md` 전면 재작성
- [ ] 6.5 `ANTIGRAVITY.md` 템플릿화

---

## Testing Strategy

### Manual Verification
- [ ] 각 워크플로우가 `/command` 형태로 인식되는지 확인
- [ ] user-rules 적용 시 에이전트 동작 확인
- [ ] 다른 프로젝트에 `.agent/` 복사 후 정상 동작 확인
- [ ] handoff → pickup 흐름 테스트

---

## Rollback Plan

1. `_archive/` 디렉토리에서 원본 복원 가능
2. `.reference/everything-claude-code/` 원본 참조 가능
3. Git history로 언제든 이전 상태 복원

---

## Timeline

| Phase | 작업 | 예상 시간 |
|-------|------|----------|
| 1 | 아카이빙 | 15min |
| 2 | Workflows | 1.5h |
| 3 | User Rules | 1.5h |
| 4 | Skills & Agents | 1h |
| 5 | Contexts | 30min |
| 6 | 문서화 | 1h |
| **Total** | | **~5.75h** |

---

## Quick Start Preview

마이그레이션 완료 후, 다른 프로젝트에서 사용하는 방법:

```bash
# 1. Workflows 복사
cp -r dotfiles-for-antigravity/.agent/workflows/ my-project/.agent/workflows/

# 2. 프로젝트 컨텍스트 복사 (필요시 수정)
cp dotfiles-for-antigravity/ANTIGRAVITY.md my-project/ANTIGRAVITY.md

# 3. (선택) 글로벌 User Rules 설정
# Antigravity 설정에서 user-rules/ 경로 지정

# 4. 사용
# /tdd, /plan, /handoff 등 바로 사용 가능
```

---

## Reference

- 원본 레포: `.reference/everything-claude-code/`
- Claude Code 가이드: [X Thread](https://x.com/affaanmustafa/status/2012378465664745795)
