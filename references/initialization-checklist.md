# 프로젝트 초기화 체크리스트

프로젝트 초기화 완료 후 이 체크리스트로 결과를 보고합니다.

## Notion 설정

- [ ] Project Hub 페이지 생성
- [ ] 프로젝트 정보 테이블 작성
  - [ ] 목표
  - [ ] 기술 스택
  - [ ] GitHub (미연결)
  - [ ] 시작일
- [ ] 📋 Specs 데이터베이스 생성
- [ ] 🤖 AI Sessions 데이터베이스 생성
- [ ] 📝 Decisions (ADR) 데이터베이스 생성
- [ ] Project Hub에 DB 인라인 삽입 완료

## GitHub 준비

- [ ] README.md 생성 (Notion 링크 포함)
- [ ] .github/PULL_REQUEST_TEMPLATE.md
- [ ] .github/ISSUE_TEMPLATE/feature.md
- [ ] .github/ISSUE_TEMPLATE/bug.md
- [ ] .github/CONTRIBUTING.md

## 결과 보고 형식

초기화 완료 후 다음 형식으로 결과를 제공:

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
- README.md
- .github/PULL_REQUEST_TEMPLATE.md
- .github/ISSUE_TEMPLATE/feature.md
- .github/ISSUE_TEMPLATE/bug.md
- .github/CONTRIBUTING.md

### 다음 단계
1. GitHub 저장소 생성 후 템플릿 파일 복사
2. Labels 설정: `spec-ready`, `in-progress`, `needs-review`, `ai-assisted`
3. Notion Project Hub의 GitHub 링크 업데이트
```

## 데이터베이스 스키마 검증

각 데이터베이스가 다음 필수 속성을 포함하는지 확인:

### 📋 Specs
- Name (Title)
- Type (Select: Feature, API, DB Schema, System Design)
- Status (Status)
- Priority (Select: Critical, High, Medium, Low)
- GitHub Issue (URL)
- Owner (Person)
- Created (Created time)
- Updated (Last edited time)

### 🤖 AI Sessions
- Name (Title)
- Purpose (Rich text)
- Session Date (Date)
- Outcome (Select: Successful, Partial, Failed, Ongoing)
- Tags (Multi-select: implementation, design, debugging, review)

### 📝 Decisions (ADR)
- Name (Title)
- Status (Select: Proposed, Accepted, Deprecated, Superseded)
- Context (Rich text)
- Decision (Rich text)
- Consequences (Rich text)
- Date (Date)
