---
layout: post
title: Understanding the Postgres EXPLAIN cost
tags: [Database]
---

**1. EXPAIN query như thế nào?**

EXPLAIN là một câu lệnh rất hữu ích trong việc tìm hiểu và tối ưu câu lệnh truy vấn của bạn khi làm việc với Postgres.
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
Kết quả trả ra là với việc scan thì cost gần như là 0.0 tuy nhiên việc sort sẽ tiêu tốn cost = 66.83. Đây là chi phí để xử lý 
dữ liệu với 1000 rows. Nếu chúng ta LIMIT lại số bản ghi thì sao?

```sql
EXPLAIN SELECT * FROM users LIMIT 1;
 
QUERY PLAN                                                    |
--------------------------------------------------------------+
Limit  (cost=0.00..0.02 rows=1 width=17)                      |
  ->  Seq Scan on users  (cost=0.00..17.00 rows=1000 width=17)|
```
Có thể thấy khi LIMIT bản ghi thì cost cho việc limit rất nhỏ, nhưng cost cho việc scan thì không thây đổi. Điều đó cho thấy chúng ta có thể optimize query dựa vào cost và thông qua việc EXPLAIN query. Vậy optimize thế nào?

**2. Optimizing queries**

