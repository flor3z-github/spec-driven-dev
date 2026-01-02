# DB Schema 템플릿

## 테이블: [table_name]

**설명**: [테이블 목적]

### 컬럼 정의

| Column | Type | Nullable | Default | Description |
|--------|------|----------|---------|-------------|
| id | UUID | No | gen_random_uuid() | PK |
| name | VARCHAR(255) | No | - | 이름 |
| status | VARCHAR(50) | No | 'active' | 상태 |
| created_at | TIMESTAMP | No | CURRENT_TIMESTAMP | 생성일시 |
| updated_at | TIMESTAMP | No | CURRENT_TIMESTAMP | 수정일시 |
| deleted_at | TIMESTAMP | Yes | NULL | 삭제일시 (soft delete) |

### 인덱스

| Name | Columns | Type | Description |
|------|---------|------|-------------|
| pk_[table]_id | id | PRIMARY | 기본키 |
| idx_[table]_status | status | BTREE | 상태 필터링 |
| idx_[table]_created | created_at | BTREE | 생성일 정렬 |

### 제약조건

| Name | Type | Definition |
|------|------|------------|
| fk_[table]_[ref] | FOREIGN KEY | REFERENCES [ref_table](id) |
| chk_[table]_status | CHECK | status IN ('active', 'inactive', 'deleted') |

### SQL

```sql
CREATE TABLE [table_name] (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    name VARCHAR(255) NOT NULL,
    status VARCHAR(50) NOT NULL DEFAULT 'active',
    created_at TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP,
    deleted_at TIMESTAMP,
    
    CONSTRAINT chk_[table]_status CHECK (status IN ('active', 'inactive', 'deleted'))
);

CREATE INDEX idx_[table]_status ON [table_name](status);
CREATE INDEX idx_[table]_created ON [table_name](created_at);
```

---

## 관계 다이어그램 (ERD)

```
[users] 1 ──── N [posts]
   │
   └──── N [comments]
             │
[posts] 1 ───┘
```

## 마이그레이션 이력

| Version | Date | Description | Status |
|---------|------|-------------|--------|
| 001 | 2024-01-01 | Initial schema | Applied |
| 002 | 2024-01-15 | Add status column | Pending |

---

## 공통 규칙

### 명명 규칙
- 테이블: snake_case, 복수형 (users, posts)
- 컬럼: snake_case (created_at, user_id)
- 인덱스: `idx_[table]_[columns]`
- FK: `fk_[table]_[ref_table]`

### 공통 컬럼
모든 테이블에 포함:
- `id`: UUID, PK
- `created_at`: TIMESTAMP
- `updated_at`: TIMESTAMP

### Soft Delete
삭제 시 `deleted_at` 컬럼 사용 (NULL이면 활성)

### Enum 대체
VARCHAR + CHECK 제약조건 사용 (enum 타입 대신)
