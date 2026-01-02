# Project Hub 템플릿

프로젝트 초기화 시 이 템플릿을 **정확히** 따라야 합니다.

## 🚨 중요: API 호출 순서

### ⛔ 절대 금지

| 금지 항목 | 이유 |
|----------|------|
| `replace_content` 명령 | 페이지의 모든 자식 블록(DB 포함) 삭제 |
| content에 `<database inline="true">` 태그 | 스키마 수정 불가 (API 미지원) |
| DB 생성 후 페이지 content 전체 수정 | 위 두 가지 유발 |

### ✅ 올바른 4단계 워크플로우

```
1. notion-create-pages     → 프로젝트 정보만 (DB 없이!)
2. notion-create-database  → 스키마와 함께 (×3)
3. notion-update-database  → is_inline: true (×3)
4. 완료! (추가 작업 없음)
```

---

## 1단계: notion-create-pages content

**content에는 DB 태그가 없어야 합니다!**

```markdown
## 프로젝트 정보

<table header-row="true">
<tr>
<td>항목</td>
<td>내용</td>
</tr>
<tr>
<td>목표</td>
<td>[프로젝트 목표 - 한 문장]</td>
</tr>
<tr>
<td>기술 스택</td>
<td>[주요 기술 나열]</td>
</tr>
<tr>
<td>GitHub</td>
<td>(미연결)</td>
</tr>
<tr>
<td>시작일</td>
<td>[YYYY-MM-DD]</td>
</tr>
</table>

---
```

## 2단계: notion-create-database (×3)

각 DB는 `notion-create-database`로 **스키마와 함께** 생성

```
parent: { "type": "page_id", "page_id": "<Project Hub ID>" }
```

### 📋 Specs DB 스키마
- Name (title)
- Type (select: Feature, API, DB Schema, System Design)
- Status (status)
- Priority (select: Critical, High, Medium, Low)
- Owner (people)
- GitHub Issue (url)
- Created (created_time)
- Updated (last_edited_time)

### 🤖 AI Sessions DB 스키마
- Name (title)
- Purpose (rich_text)
- Session Date (date)
- Outcome (select: Successful, Partial, Failed, Ongoing)
- Tags (multi_select: implementation, design, debugging, review)

### 📝 Decisions (ADR) DB 스키마
- Name (title)
- Status (select: Proposed, Accepted, Deprecated, Superseded)
- Context (rich_text)
- Decision (rich_text)
- Consequences (rich_text)
- Date (date)

## 3단계: notion-update-database (×3)

각 DB에 대해:
```json
{
  "database_id": "<DB ID>",
  "is_inline": true
}
```

## 4단계: 완료!

**⛔ 추가 content 수정 없음** - replace_content 절대 사용 금지

---

## 최종 결과 구조

```
[Project Name]
├── 프로젝트 정보 (테이블)
├── ---
├── 📋 Specs (inline, 원본, 스키마 ✓)
├── 🤖 AI Sessions (inline, 원본, 스키마 ✓)
└── 📝 Decisions (ADR) (inline, 원본, 스키마 ✓)
```

---

## 변수 설명

| 변수 | 설명 | 예시 |
|------|------|------|
| `[Project Name]` | 프로젝트 이름 | NetPulse |
| `[프로젝트 목표 - 한 문장]` | 프로젝트의 핵심 목표 | 네트워크 실시간 헬스체크 시스템 |
| `[주요 기술 나열]` | 사용 기술 스택 | Go, Redis, Elasticsearch |
| `[YYYY-MM-DD]` | 프로젝트 시작일 | 2025-01-02 |

## GitHub 연결 후 업데이트

GitHub 저장소 생성 후 `notion-update-page`의 `replace_content_range`로 GitHub 행만 업데이트:

```json
{
  "command": "replace_content_range",
  "selection_with_ellipsis": "<td>GitHub</td>...(미연결)</td>",
  "new_str": "<td>GitHub</td>\n<td>[저장소명](https://github.com/user/repo)</td>"
}
```

⚠️ `replace_content`가 아닌 `replace_content_range` 사용!