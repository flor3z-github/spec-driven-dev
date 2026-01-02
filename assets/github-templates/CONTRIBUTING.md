# Contributing Guide

## 개발 프로세스

### 1. Spec 확인

코드 작성 전 반드시 Notion Spec 확인:
- Spec 상태가 `Approved`인지 확인
- 요구사항 목록 숙지
- 불명확한 점은 Spec에 코멘트

### 2. Issue 생성/할당

- Spec URL 포함
- Label 설정: `spec-ready`
- 본인 할당

### 3. Branch 생성

```bash
# Feature
git checkout -b feature/spec-{notion-id-short}

# Bugfix
git checkout -b fix/{issue-number}-{description}

# Documentation
git checkout -b docs/{description}
```

### 4. 개발

- Spec 요구사항 기준 구현
- 주요 결정사항은 AI Session에 기록
- 테스트 코드 작성

### 5. Commit

```
<type>(<scope>): <subject>

<body>

Spec: <notion-url>
```

**Types**
| Type | Description |
|------|-------------|
| feat | 새 기능 |
| fix | 버그 수정 |
| docs | 문서 수정 |
| refactor | 리팩토링 |
| test | 테스트 |
| chore | 기타 |

**예시**
```
feat(auth): implement JWT authentication

- Add login endpoint
- Add token validation middleware
- Add refresh token logic

Spec: https://notion.so/spec-123
```

### 6. Pull Request

- PR 템플릿 작성
- Issue 연결: `Closes #123`
- Spec 링크 포함
- 리뷰어 지정

### 7. 리뷰 & 머지

- 리뷰 피드백 반영
- CI 통과 확인
- Squash merge 권장

### 8. 후처리

- Notion Spec 상태 → `Implemented`
- CHANGELOG 업데이트

---

## 코드 스타일

- ESLint/Prettier (JS/TS)
- Black/isort (Python)
- gofmt (Go)

## 테스트

```bash
# 테스트 실행
npm test        # Node.js
pytest          # Python
go test ./...   # Go
```

## 질문?

- Spec 관련: Notion 코멘트
- 코드 관련: GitHub Issue
- 긴급: 담당자 직접 연락
