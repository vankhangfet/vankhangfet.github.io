---
layout: post
title: Understanding the Postgres EXPLAIN cost
tags: [Database]
---

EPLAIN là một câu lệnh rất hữu ích trong việc tìm hiểu và tối ưu câu lệnh truy vấn của bạn khi làm việc với Postgres.
Do đó chúng ta cần hiểu kết quả của câu lệnh EXPLAIN.

Chúng ta hãy xem xét ví dụ sau. Giả sử chúng ta có dữ liệu user như dưới đây. Đoạn sql sẽ tạo ra table user với 1000 records.

```sql
CREATE TABLE users (
    id bigint GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    username text NOT NULL);
INSERT INTO users (username)
SELECT 'person' || n
FROM generate_series(1, 1000) AS n;
ANALYZE users;
```
Chúng ta sẽ thực hiện EXPLAIN một truy vấn đơn giản sau: 
```sql
EXPLAIN SELECT * FROM users ORDER BY username;
 
QUERY PLAN                                                    |
--------------------------------------------------------------+
Sort  (cost=66.83..69.33 rows=1000 width=17)                  |
  Sort Key: username                                          |
  ->  Seq Scan on users  (cost=0.00..17.00 rows=1000 width=17)|
```


