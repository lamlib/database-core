# Bảng So Sánh Chi Tiết Các DBMS Phổ Biến

## 1. AUTO INCREMENT / IDENTITY

| DBMS | Cú pháp | Ví dụ |
|------|---------|-------|
| **MySQL** | `AUTO_INCREMENT` | `id INT AUTO_INCREMENT PRIMARY KEY` |
| **PostgreSQL** | `SERIAL` hoặc `GENERATED AS IDENTITY` | `id SERIAL PRIMARY KEY`<br>`id INT GENERATED ALWAYS AS IDENTITY` |
| **SQL Server** | `IDENTITY(start, increment)` | `id INT IDENTITY(1,1) PRIMARY KEY` |
| **Oracle** | `GENERATED AS IDENTITY` (12c+)<br>hoặc SEQUENCE | `id NUMBER GENERATED ALWAYS AS IDENTITY`<br>`id NUMBER DEFAULT seq.NEXTVAL` |

---

## 2. KIỂU DỮ LIỆU CHUỖI

| DBMS | Kiểu cố định | Kiểu động | Kiểu lớn | Unicode |
|------|--------------|-----------|----------|---------|
| **MySQL** | `CHAR(n)` | `VARCHAR(n)` | `TEXT`, `LONGTEXT` | Dùng charset utf8mb4 |
| **PostgreSQL** | `CHAR(n)` | `VARCHAR(n)`, `TEXT` | `TEXT` (không giới hạn) | Mặc định UTF-8 |
| **SQL Server** | `CHAR(n)` | `VARCHAR(n)` | `VARCHAR(MAX)` | `NCHAR`, `NVARCHAR` |
| **Oracle** | `CHAR(n)` | `VARCHAR2(n)` | `CLOB` | `NCHAR`, `NVARCHAR2` |

---

## 3. KIỂU DỮ LIỆU BOOLEAN

| DBMS | Kiểu dữ liệu | Giá trị | Ví dụ |
|------|--------------|---------|--------|
| **MySQL** | `BOOLEAN` = `TINYINT(1)` | 0, 1 | `is_active BOOLEAN DEFAULT TRUE` |
| **PostgreSQL** | `BOOLEAN` | `TRUE`, `FALSE`, `NULL` | `is_active BOOLEAN DEFAULT TRUE` |
| **SQL Server** | `BIT` | 0, 1 | `is_active BIT DEFAULT 1` |
| **Oracle** | Không có - dùng `NUMBER(1)` hoặc `CHAR(1)` | 0, 1 hoặc 'Y', 'N' | `is_active NUMBER(1) CHECK (is_active IN (0,1))` |

---

## 4. KIỂU DỮ LIỆU NGÀY GIỜ

| DBMS | Date | Time | DateTime | Timestamp |
|------|------|------|----------|-----------|
| **MySQL** | `DATE` | `TIME` | `DATETIME` | `TIMESTAMP` |
| **PostgreSQL** | `DATE` | `TIME` | `TIMESTAMP` | `TIMESTAMPTZ` (with timezone) |
| **SQL Server** | `DATE` | `TIME` | `DATETIME`, `DATETIME2` | `DATETIMEOFFSET` |
| **Oracle** | `DATE` | `TIMESTAMP` | `TIMESTAMP` | `TIMESTAMP WITH TIME ZONE` |

---

## 5. HÀM NGÀY GIỜ HIỆN TẠI

| DBMS | Hàm hiện tại | Cộng ngày | Trừ ngày | Chênh lệch |
|------|--------------|-----------|----------|------------|
| **MySQL** | `NOW()`, `CURDATE()` | `DATE_ADD(date, INTERVAL 1 DAY)` | `DATE_SUB(date, INTERVAL 1 DAY)` | `DATEDIFF(date1, date2)` |
| **PostgreSQL** | `NOW()`, `CURRENT_DATE` | `date + INTERVAL '1 day'` | `date - INTERVAL '1 day'` | `date1 - date2` |
| **SQL Server** | `GETDATE()`, `GETUTCDATE()` | `DATEADD(day, 1, date)` | `DATEADD(day, -1, date)` | `DATEDIFF(day, date1, date2)` |
| **Oracle** | `SYSDATE`, `CURRENT_DATE` | `date + INTERVAL '1' DAY` | `date - INTERVAL '1' DAY` | `date1 - date2` |

---

## 6. HÀM CHUỖI

| Chức năng | MySQL | PostgreSQL | SQL Server | Oracle |
|-----------|-------|------------|------------|--------|
| **Nối chuỗi** | `CONCAT()` hoặc `\|\|` | `\|\|` hoặc `CONCAT()` | `+` hoặc `CONCAT()` | `\|\|` hoặc `CONCAT()` |
| **Độ dài** | `LENGTH()` | `LENGTH()` | `LEN()` | `LENGTH()` |
| **Chữ HOA** | `UPPER()` | `UPPER()` | `UPPER()` | `UPPER()` |
| **Chữ thường** | `LOWER()` | `LOWER()` | `LOWER()` | `LOWER()` |
| **Cắt khoảng trắng** | `TRIM()` | `TRIM()` | `TRIM()` | `TRIM()` |
| **Substring** | `SUBSTRING(str, pos, len)` | `SUBSTRING(str, pos, len)` | `SUBSTRING(str, pos, len)` | `SUBSTR(str, pos, len)` |
| **Thay thế** | `REPLACE()` | `REPLACE()` | `REPLACE()` | `REPLACE()` |

---

## 7. PHÂN TRANG (LIMIT / OFFSET)

| DBMS | Cú pháp | Ví dụ lấy 10 bản ghi từ vị trí 20 |
|------|---------|-----------------------------------|
| **MySQL** | `LIMIT offset, count` hoặc `LIMIT count OFFSET offset` | `SELECT * FROM users LIMIT 20, 10`<br>`SELECT * FROM users LIMIT 10 OFFSET 20` |
| **PostgreSQL** | `LIMIT count OFFSET offset` | `SELECT * FROM users LIMIT 10 OFFSET 20` |
| **SQL Server** | `OFFSET rows FETCH NEXT rows ONLY` | `SELECT * FROM users ORDER BY id`<br>`OFFSET 20 ROWS FETCH NEXT 10 ROWS ONLY` |
| **Oracle** | `OFFSET rows FETCH NEXT rows ONLY` (12c+) | `SELECT * FROM users ORDER BY id`<br>`OFFSET 20 ROWS FETCH NEXT 10 ROWS ONLY` |

---

## 8. UPSERT (INSERT OR UPDATE)

| DBMS | Cú pháp |
|------|---------|
| **MySQL** | `INSERT ... ON DUPLICATE KEY UPDATE` |
| **PostgreSQL** | `INSERT ... ON CONFLICT ... DO UPDATE` |
| **SQL Server** | `MERGE INTO ... WHEN MATCHED ... WHEN NOT MATCHED` |
| **Oracle** | `MERGE INTO ... WHEN MATCHED ... WHEN NOT MATCHED` |

**Ví dụ MySQL:**
```sql
INSERT INTO users (id, name, email) 
VALUES (1, 'John', 'john@example.com')
ON DUPLICATE KEY UPDATE name = VALUES(name);
```

**Ví dụ PostgreSQL:**
```sql
INSERT INTO users (id, name, email) 
VALUES (1, 'John', 'john@example.com')
ON CONFLICT (id) DO UPDATE 
SET name = EXCLUDED.name;
```

---

## 9. CHECK TABLE / DROP TABLE IF EXISTS

| DBMS | DROP IF EXISTS | CREATE IF NOT EXISTS | Check table exists |
|------|----------------|----------------------|-------------------|
| **MySQL** | `DROP TABLE IF EXISTS tbl` | `CREATE TABLE IF NOT EXISTS tbl` | `SHOW TABLES LIKE 'tbl'` |
| **PostgreSQL** | `DROP TABLE IF EXISTS tbl` | `CREATE TABLE IF NOT EXISTS tbl` | `SELECT FROM pg_tables WHERE tablename='tbl'` |
| **SQL Server** | `IF OBJECT_ID('tbl','U') IS NOT NULL DROP TABLE tbl` | `IF NOT EXISTS (SELECT * FROM sys.tables WHERE name='tbl')` | `SELECT * FROM sys.tables WHERE name='tbl'` |
| **Oracle** | Cần PL/SQL block | Cần PL/SQL block | `SELECT * FROM user_tables WHERE table_name='TBL'` |

---

## 10. CONSTRAINTS - CÚ PHÁP

| Constraint | Tất cả DBMS (tương tự) |
|------------|------------------------|
| **PRIMARY KEY** | `id INT PRIMARY KEY`<br>`CONSTRAINT pk_name PRIMARY KEY (id)` |
| **FOREIGN KEY** | `FOREIGN KEY (user_id) REFERENCES users(id)`<br>`ON DELETE CASCADE / SET NULL / NO ACTION` |
| **UNIQUE** | `email VARCHAR(255) UNIQUE`<br>`CONSTRAINT uq_name UNIQUE (email)` |
| **CHECK** | `price DECIMAL CHECK (price > 0)`<br>`CONSTRAINT chk_name CHECK (price > 0)` |
| **NOT NULL** | `name VARCHAR(100) NOT NULL` |
| **DEFAULT** | `status VARCHAR(20) DEFAULT 'active'` |

---

## 11. JSON SUPPORT

| DBMS | Kiểu dữ liệu | Truy vấn | Ví dụ |
|------|--------------|----------|--------|
| **MySQL** | `JSON` | `JSON_EXTRACT()`, `->`, `->>` | `SELECT data->>'$.name' FROM tbl` |
| **PostgreSQL** | `JSON`, `JSONB` | `->`, `->>`, `@>`, `?` | `SELECT data->>'name' FROM tbl` |
| **SQL Server** | `NVARCHAR` + JSON functions | `JSON_VALUE()`, `JSON_QUERY()` | `SELECT JSON_VALUE(data, '$.name')` |
| **Oracle** | `CLOB`, `JSON` (21c) | `JSON_VALUE()`, `JSON_QUERY()` | `SELECT JSON_VALUE(data, '$.name')` |

---

## 12. WINDOW FUNCTIONS

| Chức năng | MySQL | PostgreSQL | SQL Server | Oracle |
|-----------|-------|------------|------------|--------|
| **ROW_NUMBER()** | ✅ (8.0+) | ✅ | ✅ | ✅ |
| **RANK()** | ✅ (8.0+) | ✅ | ✅ | ✅ |
| **DENSE_RANK()** | ✅ (8.0+) | ✅ | ✅ | ✅ |
| **LEAD() / LAG()** | ✅ (8.0+) | ✅ | ✅ | ✅ |
| **FIRST_VALUE()** | ✅ (8.0+) | ✅ | ✅ | ✅ |

**Ví dụ (tất cả DBMS):**
```sql
SELECT 
    name,
    salary,
    ROW_NUMBER() OVER (ORDER BY salary DESC) as row_num,
    RANK() OVER (ORDER BY salary DESC) as rank
FROM employees;
```

---

## 13. RECURSIVE QUERIES (CTE)

| DBMS | Hỗ trợ | Cú pháp |
|------|--------|---------|
| **MySQL** | ✅ (8.0+) | `WITH cte AS (...)` (không cần RECURSIVE) |
| **PostgreSQL** | ✅ | `WITH RECURSIVE cte AS (...)` |
| **SQL Server** | ✅ | `WITH cte AS (...)` (không cần RECURSIVE) |
| **Oracle** | ✅ | `WITH cte AS (...)` (không cần RECURSIVE) |

---

## 14. TOP N QUERIES

| DBMS | Cú pháp | Ví dụ lấy 10 bản ghi đầu |
|------|---------|--------------------------|
| **MySQL** | `LIMIT` | `SELECT * FROM users ORDER BY id LIMIT 10` |
| **PostgreSQL** | `LIMIT` | `SELECT * FROM users ORDER BY id LIMIT 10` |
| **SQL Server** | `TOP` | `SELECT TOP 10 * FROM users ORDER BY id` |
| **Oracle** | `FETCH FIRST` hoặc `ROWNUM` | `SELECT * FROM users ORDER BY id FETCH FIRST 10 ROWS ONLY` |

---

## 15. TRANSACTION ISOLATION LEVELS

| Level | MySQL | PostgreSQL | SQL Server | Oracle |
|-------|-------|------------|------------|--------|
| **READ UNCOMMITTED** | ✅ | ❌ | ✅ | ❌ |
| **READ COMMITTED** | ✅ | ✅ (default) | ✅ (default) | ✅ (default) |
| **REPEATABLE READ** | ✅ (default) | ✅ | ✅ | ❌ |
| **SERIALIZABLE** | ✅ | ✅ | ✅ | ✅ |

---

## 16. FULL TEXT SEARCH

| DBMS | Hỗ trợ | Cú pháp |
|------|--------|---------|
| **MySQL** | ✅ FULLTEXT index | `MATCH(column) AGAINST('search')` |
| **PostgreSQL** | ✅ tsvector/tsquery | `to_tsvector(column) @@ to_tsquery('search')` |
| **SQL Server** | ✅ FULLTEXT index | `CONTAINS(column, 'search')` |
| **Oracle** | ✅ Oracle Text | `CONTAINS(column, 'search') > 0` |

---

## 17. BACKUP & RESTORE

| DBMS | Backup Command | Restore Command |
|------|----------------|-----------------|
| **MySQL** | `mysqldump` | `mysql < backup.sql` |
| **PostgreSQL** | `pg_dump` | `psql < backup.sql` |
| **SQL Server** | `BACKUP DATABASE` | `RESTORE DATABASE` |
| **Oracle** | `expdp` hoặc RMAN | `impdp` hoặc RMAN |

---

## 18. ĐIỂM KHÁC BIỆT CHÍNH

| Đặc điểm | MySQL | PostgreSQL | SQL Server | Oracle |
|----------|-------|------------|------------|--------|
| **Giấy phép** | Open Source (GPL) | Open Source (PostgreSQL) | Proprietary (Microsoft) | Proprietary (Oracle) |
| **Nền tảng** | Cross-platform | Cross-platform | Windows, Linux | Cross-platform |
| **Phù hợp cho** | Web apps, đơn giản | Complex queries, compliance | Windows ecosystem | Enterprise lớn |
| **Tuân thủ SQL Standard** | Trung bình | Cao nhất | Trung bình | Cao |
| **Hiệu năng đọc** | Rất tốt | Tốt | Tốt | Xuất sắc |
| **Hiệu năng ghi** | Tốt | Rất tốt | Tốt | Xuất sắc |
| **Dễ học** | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐ |
| **Chi phí** | Miễn phí | Miễn phí | Có phí (Standard, Enterprise) | Rất đắt |
