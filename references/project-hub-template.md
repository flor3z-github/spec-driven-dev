# Project Hub 템플릿

프로젝트 초기화 시 이 템플릿을 **정확히** 따라야 합니다.

## Notion 페이지 구조

```
# [Project Name]

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

<database inline="true">📋 Specs</database>

<database inline="true">🤖 AI Sessions</database>

<database inline="true">📝 Decisions (ADR)</database>
```

## 필수 규칙

1. **프로젝트 정보는 반드시 테이블 형식**
   - 불릿 포인트 목록 사용 금지
   - 4개 필드 필수: 목표, 기술 스택, GitHub, 시작일

2. **구분선 위치**
   - 프로젝트 정보 테이블 직후 `---` 하나만 사용
   - 데이터베이스들 사이에는 구분선 없음

3. **데이터베이스 순서 고정**
   - 📋 Specs → 🤖 AI Sessions → 📝 Decisions (ADR)
   - 모두 inline="true" 설정

4. **섹션 헤더**
   - "프로젝트 정보" 섹션만 존재
   - "데이터베이스", "빠른 링크" 등 별도 섹션 헤더 없음

## 변수 설명

| 변수 | 설명 | 예시 |
|------|------|------|
| `[Project Name]` | 프로젝트 이름 | NetPulse - Real-time Network Health Monitor |
| `[프로젝트 목표 - 한 문장]` | 프로젝트의 핵심 목표 | 네트워크 인프라의 실시간 헬스체크 및 이상 탐지 시스템 |
| `[주요 기술 나열]` | 사용 기술 스택 | Go, Redis, Elasticsearch, Prometheus |
| `[YYYY-MM-DD]` | 프로젝트 시작일 | 2025-01-02 |

## GitHub 연결 후 업데이트

GitHub 저장소 생성 후 테이블의 GitHub 행을 업데이트:

```
<td>GitHub</td>
<td>[저장소명](https://github.com/user/repo)</td>
```
