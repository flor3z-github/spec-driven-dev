# Notion 스키마 정의

> ⚠️ **중요**: 모든 DB는 `notion-create-database`로 생성해야 합니다.
> `<database inline="true">` 태그로 생성하면 스키마 수정이 불가능합니다.

---

## 📋 Specs Database

| Property | Type | Options | Description |
|----------|------|---------|-------------|
| Name | title | - | Spec 제목 |
| Type | select | `Feature`, `API`, `DB Schema`, `System Design` | Spec 유형 |
| Status | status | (Notion 기본값) | 진행 상태 |
| Priority | select | `Critical`, `High`, `Medium`, `Low` | 우선순위 |
| Owner | people | - | 담당자 |
| GitHub Issue | url | - | 연결된 Issue URL |
| Created | created_time | - | 생성일 (자동) |
| Updated | last_edited_time | - | 수정일 (자동) |

### notion-create-database 호출 예시

```json
{
  "parent": {"type": "page_id", "page_id": "<Project Hub ID>"},
  "title": [{"text": {"content": "📋 Specs"}, "type": "text"}],
  "properties": {
    "Name": {"type": "title", "title": {}},
    "Type": {"type": "select", "select": {"options": [
      {"name": "Feature", "color": "blue"},
      {"name": "API", "color": "green"},
      {"name": "DB Schema", "color": "purple"},
      {"name": "System Design", "color": "orange"}
    ]}},
    "Status": {"type": "status", "status": {}},
    "Priority": {"type": "select", "select": {"options": [
      {"name": "Critical", "color": "red"},
      {"name": "High", "color": "orange"},
      {"name": "Medium", "color": "yellow"},
      {"name": "Low", "color": "gray"}
    ]}},
    "Owner": {"type": "people", "people": {}},
    "GitHub Issue": {"type": "url", "url": {}},
    "Created": {"type": "created_time", "created_time": {}},
    "Updated": {"type": "last_edited_time", "last_edited_time": {}}
  }
}
```

### 상태 전환 규칙

```
Draft → Review: Spec 작성 완료, 검토 요청
Review → Approved: 검토 완료, 구현 가능
Approved → Implemented: 코드 구현 완료 (PR Merged)
Any → Deprecated: 더 이상 유효하지 않음
```

---

## 🤖 AI Sessions Database

| Property | Type | Options | Description |
|----------|------|---------|-------------|
| Name | title | - | 세션 제목 |
| Purpose | rich_text | - | 세션 목적 |
| Session Date | date | - | 세션 날짜 |
| Outcome | select | `Successful`, `Partial`, `Failed`, `Ongoing` | 결과 |
| Tags | multi_select | `implementation`, `design`, `debugging`, `review` | 태그 |

### notion-create-database 호출 예시

```json
{
  "parent": {"type": "page_id", "page_id": "<Project Hub ID>"},
  "title": [{"text": {"content": "🤖 AI Sessions"}, "type": "text"}],
  "properties": {
    "Name": {"type": "title", "title": {}},
    "Purpose": {"type": "rich_text", "rich_text": {}},
    "Session Date": {"type": "date", "date": {}},
    "Outcome": {"type": "select", "select": {"options": [
      {"name": "Successful", "color": "green"},
      {"name": "Partial", "color": "yellow"},
      {"name": "Failed", "color": "red"},
      {"name": "Ongoing", "color": "blue"}
    ]}},
    "Tags": {"type": "multi_select", "multi_select": {"options": [
      {"name": "implementation", "color": "blue"},
      {"name": "design", "color": "purple"},
      {"name": "debugging", "color": "red"},
      {"name": "review", "color": "green"}
    ]}}
  }
}
```

---

## 📝 Decisions Database (ADR)

| Property | Type | Options | Description |
|----------|------|---------|-------------|
| Name | title | - | 결정 제목 |
| Status | select | `Proposed`, `Accepted`, `Deprecated`, `Superseded` | 상태 |
| Context | rich_text | - | 배경/상황 |
| Decision | rich_text | - | 결정 내용 |
| Consequences | rich_text | - | 예상 결과 |
| Date | date | - | 결정 날짜 |

### notion-create-database 호출 예시

```json
{
  "parent": {"type": "page_id", "page_id": "<Project Hub ID>"},
  "title": [{"text": {"content": "📝 Decisions (ADR)"}, "type": "text"}],
  "properties": {
    "Name": {"type": "title", "title": {}},
    "Status": {"type": "select", "select": {"options": [
      {"name": "Proposed", "color": "yellow"},
      {"name": "Accepted", "color": "green"},
      {"name": "Deprecated", "color": "gray"},
      {"name": "Superseded", "color": "orange"}
    ]}},
    "Context": {"type": "rich_text", "rich_text": {}},
    "Decision": {"type": "rich_text", "rich_text": {}},
    "Consequences": {"type": "rich_text", "rich_text": {}},
    "Date": {"type": "date", "date": {}}
  }
}
```

---

## 최종 Project Hub 구조

```
[Project Name]
├── 프로젝트 정보 (테이블)
│   ├── 목표
│   ├── 기술 스택
│   ├── GitHub
│   └── 시작일
├── ---
├── 📋 Specs (inline, 원본)
├── 🤖 AI Sessions (inline, 원본)
└── 📝 Decisions (ADR) (inline, 원본)
```

### ⛔ 금지된 구조

```
❌ 불릿 포인트 프로젝트 정보
❌ "데이터베이스" 섹션 헤더
❌ "빠른 링크" 섹션
❌ linked view (원본만 사용)
```