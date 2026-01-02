---
name: spec-driven-dev
description: "AI 기반 Spec Driven Development 워크플로우. Notion(문서/Spec)과 GitHub(코드) 통합 관리. 사용 시점: (1) 새 프로젝트 시작, (2) Feature Spec 작성, (3) Spec을 코드로 구현, (4) PR 생성, (5) AI 세션 기록. Notion MCP와 GitHub MCP 연동 필수."
---

# Spec Driven Development

Notion을 Spec 허브로, GitHub를 코드 허브로 사용하는 AI 기반 개발 워크플로우.

## 워크플로우 결정 트리

```
사용자 요청 분석:
├── "새 프로젝트 시작" → 프로젝트 초기화 워크플로우
├── "기능 추가/개발" → Feature 개발 워크플로우
├── "Spec 작성" → Spec 문서화 워크플로우
├── "구현하자" → Spec→Code 워크플로우
├── "PR 만들어줘" → PR 생성 워크플로우
└── "세션 기록" → AI Session 로깅
```

## 핵심 원칙

1. **Spec First**: 코드 작성 전 반드시 Spec 문서 확인/작성
2. **Single Source of Truth**: Notion=문서, GitHub=코드 (중복 금지)
3. **Traceability**: 모든 코드는 Spec과 연결, 모든 PR은 Issue와 연결
4. **AI Transparency**: AI 협업 내용은 AI Session에 기록
5. **Structural Consistency**: 모든 프로젝트는 동일한 구조를 따름

## AI 실행 지침

### 프로젝트 초기화 시 필수 준수사항

1. **Project Hub 구조**
   - **반드시** [project-hub-template.md](references/project-hub-template.md) 템플릿 사용
   - 프로젝트 정보는 **테이블 형식만 허용** (불릿 목록 금지)
   - 필수 필드: 목표, 기술 스택, GitHub, 시작일
   - 시작일은 **현재 날짜** 자동 입력

2. **데이터베이스 생성 순서**
   - 📋 Specs → 🤖 AI Sessions → 📝 Decisions (ADR)
   - 생성 후 **반드시** Project Hub에 inline 삽입
   - 스키마는 [notion-schema.md](references/notion-schema.md) 정확히 준수

3. **결과 보고**
   - [initialization-checklist.md](references/initialization-checklist.md)의 형식으로 보고
   - 모든 URL 포함 필수

### 구조 일관성 규칙

```
✅ 허용:
- 테이블 형식 프로젝트 정보
- 단일 구분선 (프로젝트 정보 후)
- DB 3개 순차 배치 (Specs → AI Sessions → Decisions)

❌ 금지:
- 불릿 포인트 프로젝트 정보
- "데이터베이스", "빠른 링크" 등 추가 섹션 헤더
- DB 순서 변경
- 구분선 추가
```

## 프로젝트 초기화

새 프로젝트 시작 시 다음 순서대로 **정확히** 진행:

### 1단계: Notion Project Hub 생성

```
필수 입력 정보:
- 프로젝트명
- 목표 (한 문장)
- 기술 스택
- 시작일 (현재 날짜)
```

**Notion 페이지 구조** ([project-hub-template.md](references/project-hub-template.md) 참조):

```markdown
# [Project Name]

## 프로젝트 정보
<table header-row="true">
<tr><td>항목</td><td>내용</td></tr>
<tr><td>목표</td><td>[프로젝트 목표]</td></tr>
<tr><td>기술 스택</td><td>[기술 나열]</td></tr>
<tr><td>GitHub</td><td>(미연결)</td></tr>
<tr><td>시작일</td><td>[YYYY-MM-DD]</td></tr>
</table>

---

<database inline="true">📋 Specs</database>
<database inline="true">🤖 AI Sessions</database>
<database inline="true">📝 Decisions (ADR)</database>
```

### 2단계: 데이터베이스 생성

Project Hub 하위에 순서대로 생성:

| 순서 | 데이터베이스 | 스키마 참조 |
|------|-------------|------------|
| 1 | 📋 Specs | [notion-schema.md#specs-database](references/notion-schema.md) |
| 2 | 🤖 AI Sessions | [notion-schema.md#ai-sessions-database](references/notion-schema.md) |
| 3 | 📝 Decisions (ADR) | [notion-schema.md#decisions-database](references/notion-schema.md) |

### 3단계: Project Hub 업데이트

생성된 데이터베이스들을 Project Hub에 inline으로 삽입

### 4단계: GitHub 템플릿 준비

```
/home/claude/[project-name]/
├── README.md                          # Notion 링크 포함
└── .github/
    ├── PULL_REQUEST_TEMPLATE.md
    ├── CONTRIBUTING.md
    └── ISSUE_TEMPLATE/
        ├── feature.md
        └── bug.md
```

템플릿 소스: [github-templates](assets/github-templates/)

### 5단계: 결과 보고

[initialization-checklist.md](references/initialization-checklist.md) 형식으로 결과 제공:

```markdown
## ✅ 프로젝트 초기화 완료

### Notion
| 구성요소 | URL |
|---------|-----|
| Project Hub | [프로젝트명](URL) |
| 📋 Specs | [링크](URL) |
| 🤖 AI Sessions | [링크](URL) |
| 📝 Decisions | [링크](URL) |

### GitHub 템플릿
(파일 목록)

### 다음 단계
1. GitHub 저장소 생성 후 템플릿 파일 복사
2. Labels 설정: `spec-ready`, `in-progress`, `needs-review`, `ai-assisted`
3. Notion Project Hub의 GitHub 링크 업데이트
```

## Feature 개발 워크플로우

```
1. Spec 작성 (Notion)
   └── Feature Spec 템플릿 사용
   └── 상태: Draft

2. Spec 검토
   └── 상태: Draft → Review → Approved

3. GitHub Issue 생성
   └── Spec URL 포함
   └── Label: spec-ready

4. Branch 생성
   └── 명명: feature/spec-{notion-page-id-short}

5. 구현
   └── AI Session 기록 (주요 결정사항)

6. PR 생성
   └── Issue 연결 (Closes #N)
   └── Spec 링크 포함

7. Merge 후
   └── Notion Spec 상태: Implemented
   └── CHANGELOG 업데이트
```

## Spec 문서 템플릿

### Feature Spec
```markdown
# [Feature Name]

## 개요
[한 문장 설명]

## 배경/목적
[왜 필요한가]

## 요구사항
### 기능 요구사항
- [ ] FR-1: ...
- [ ] FR-2: ...

### 비기능 요구사항
- [ ] NFR-1: ...

## 기술 설계
### API 변경사항
[API Spec 링크 또는 간단 명세]

### DB 변경사항
[DB Schema 링크 또는 간단 명세]

## 테스트 시나리오
- TC-1: ...
- TC-2: ...

## 관련 문서
- GitHub Issue: [링크]
- 관련 Spec: [링크]
```

### API Spec
[api-spec-template.md](references/api-spec-template.md) 참조

### DB Schema
[db-schema-template.md](references/db-schema-template.md) 참조

## GitHub 연동 규칙

### Commit Message
```
<type>(<scope>): <subject>

[body]

[footer]
Spec: <notion-spec-url>
```

Types: `feat`, `fix`, `docs`, `refactor`, `test`, `chore`

### Branch 명명
- Feature: `feature/spec-{id}` 또는 `feature/{short-desc}`
- Bugfix: `fix/{issue-number}-{short-desc}`
- Docs: `docs/{short-desc}`

### PR 템플릿
[PULL_REQUEST_TEMPLATE.md](assets/github-templates/PULL_REQUEST_TEMPLATE.md) 참조

## AI Session 기록

AI와 협업 시 주요 내용을 Notion AI Sessions DB에 기록:

```markdown
# [Session 제목]

## 목적
[이 세션에서 달성하려는 것]

## 컨텍스트
[관련 Spec/Issue 링크]

## 주요 프롬프트
[핵심 프롬프트 기록]

## 결과 요약
[AI가 생성한 주요 결과물]

## 의사결정
[세션 중 내린 결정사항]

## 후속 작업
- [ ] ...
```

## 도구 사용

### Notion MCP
- `notion-search`: Spec 검색
- `notion-fetch`: 페이지/DB 조회
- `notion-create-pages`: Spec 생성
- `notion-update-page`: 상태 업데이트

### GitHub MCP (연결 시)
- Issue 생성/조회
- PR 생성
- 파일 커밋

## 참조 문서

- [Project Hub 템플릿](references/project-hub-template.md) ⭐ 프로젝트 초기화 필수
- [초기화 체크리스트](references/initialization-checklist.md) ⭐ 결과 보고 형식
- [Notion 스키마 정의](references/notion-schema.md)
- [API Spec 템플릿](references/api-spec-template.md)
- [DB Schema 템플릿](references/db-schema-template.md)
- [GitHub 템플릿](assets/github-templates/)
