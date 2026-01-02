# API Spec 템플릿

## 엔드포인트 정의

### [HTTP Method] /api/v1/resource

**설명**: [API 목적]

**인증**: Required / Optional / None

#### Request

**Headers**
| Header | Required | Description |
|--------|----------|-------------|
| Authorization | Yes | Bearer {token} |
| Content-Type | Yes | application/json |

**Path Parameters**
| Parameter | Type | Description |
|-----------|------|-------------|
| id | string | 리소스 ID |

**Query Parameters**
| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| page | integer | No | 1 | 페이지 번호 |
| limit | integer | No | 20 | 페이지당 개수 |

**Request Body**
```json
{
  "field1": "string (required) - 설명",
  "field2": 0,
  "nested": {
    "subfield": "string"
  }
}
```

#### Response

**Success (200 OK)**
```json
{
  "success": true,
  "data": {
    "id": "uuid",
    "field1": "value",
    "createdAt": "2024-01-01T00:00:00Z"
  }
}
```

**Error Responses**
| Status | Code | Message |
|--------|------|---------|
| 400 | INVALID_REQUEST | 요청 형식 오류 |
| 401 | UNAUTHORIZED | 인증 필요 |
| 404 | NOT_FOUND | 리소스 없음 |
| 500 | INTERNAL_ERROR | 서버 오류 |

```json
{
  "success": false,
  "error": {
    "code": "ERROR_CODE",
    "message": "Error description"
  }
}
```

---

## API 목록 요약

| Method | Endpoint | Description | Status |
|--------|----------|-------------|--------|
| GET | /api/v1/resources | 목록 조회 | Draft |
| POST | /api/v1/resources | 생성 | Draft |
| GET | /api/v1/resources/:id | 상세 조회 | Draft |
| PUT | /api/v1/resources/:id | 수정 | Draft |
| DELETE | /api/v1/resources/:id | 삭제 | Draft |

---

## 공통 규칙

### 응답 형식
모든 응답은 다음 구조를 따름:
```json
{
  "success": boolean,
  "data": object | array | null,
  "error": object | null,
  "meta": {
    "page": number,
    "limit": number,
    "total": number
  }
}
```

### 날짜/시간
- ISO 8601 형식 사용: `YYYY-MM-DDTHH:mm:ssZ`
- 모든 시간은 UTC 기준

### 페이지네이션
- `page`: 1부터 시작
- `limit`: 기본값 20, 최대 100
- 응답의 `meta` 객체에 페이지 정보 포함
