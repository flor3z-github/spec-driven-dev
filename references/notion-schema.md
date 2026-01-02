# Notion 스키마 정의

## Specs Database

| Property | Type | Options/Description |
|----------|------|---------------------|
| Name | Title | Spec 제목 |
| Type | Select | `Feature`, `API`, `DB Schema`, `System Design` |
| Status | Status | `Draft` → `Review` → `Approved` → `Implemented` → `Deprecated` |
| Priority | Select | `Critical`, `High`, `Medium`, `Low` |
| GitHub Issue | URL | 연결된 GitHub Issue URL |
| Related Specs | Relation | 다른 Spec 연결 |
| Owner | Person | 담당자 |
| Created | Created time | 자동 |
| Updated | Last edited time | 자동 |

### 상태 전환 규칙
```
Draft → Review: Spec 작성 완료, 검토 요청
Review → Approved: 검토 완료, 구현 가능
Approved → Implemented: 코드 구현 완료 (PR Merged)
Any → Deprecated: 더 이상 유효하지 않음
```

## AI Sessions Database

| Property | Type | Description |
|----------|------|-------------|
| Name | Title | 세션 제목 |
| Purpose | Rich text | 세션 목적 |
| Related Spec | Relation | Specs DB 연결 |
| Session Date | Date | 세션 날짜 |
| Outcome | Select | `Successful`, `Partial`, `Failed`, `Ongoing` |
| Tags | Multi-select | `implementation`, `design`, `debugging`, `review` |

## Decisions Database (ADR)

| Property | Type | Description |
|----------|------|-------------|
| Name | Title | 결정 제목 |
| Status | Select | `Proposed`, `Accepted`, `Deprecated`, `Superseded` |
| Context | Rich text | 배경/상황 |
| Decision | Rich text | 결정 내용 |
| Consequences | Rich text | 예상 결과 |
| Related Spec | Relation | Specs DB 연결 |
| Date | Date | 결정 날짜 |

## Project Overview Page

프로젝트 루트 페이지 구조:
```
# [Project Name]

## 프로젝트 정보
- 목표: ...
- 기술 스택: ...
- GitHub: [저장소 링크]

## 데이터베이스
- 📋 Specs (inline database)
- 🤖 AI Sessions (inline database)  
- 📝 Decisions (inline database)

## 빠른 링크
- 현재 진행 중: [필터링된 Specs 뷰]
- 최근 AI 세션: [필터링된 AI Sessions 뷰]
```
