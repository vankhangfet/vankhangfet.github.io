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
Trong phần này mình sẽ tham khảo ví dụ của Gitlab, chúng ta giả định query như sau: 

```sql
EXPLAIN (ANALYZE, BUFFERS)
SELECT COUNT(*)
FROM users
WHERE twitter != '';
```
Kết quả truy vấn như sau:
```sql
Aggregate  (cost=845110.21..845110.22 rows=1 width=8) (actual time=1271.157..1271.158 rows=1 loops=1)
  Buffers: shared hit=202662
  ->  Seq Scan on users  (cost=0.00..844969.99 rows=56087 width=0) (actual time=0.019..1265.883 rows=51833 loops=1)
        Filter: ((twitter)::text <> ''::text)
        Rows Removed by Filter: 2487813
        Buffers: shared hit=202662
Planning time: 0.390 ms
Execution time: 1271.180 ms
```
Từ kết quả query sau chúng ta có thể thấy rằng việc truy vấn user tốn khá nhiều chi phí.
1. Thực hiện scan table user
2. Việc filter user thực hiện loại bỏ 2487813 rows
3. Câu truy vấn này cần sử dụng buffers là 202,622 tương đương với sử dụng 1.58 GB bộ nhớ.

Vậy chúng ta thực hiện tối ưu câu truy vấn này thế nào? Việc chúng ta hay nghĩ đến đó là thực hiện index 

```sql
CREATE INDEX CONCURRENTLY twitter_test ON users (twitter);
```
Sau đó thực hiện chay lại EXPLAIN query và xem kết quả:

```sql
Aggregate  (cost=61002.82..61002.83 rows=1 width=8) (actual time=297.311..297.312 rows=1 loops=1)
  Buffers: shared hit=51854 dirtied=19
  ->  Index Only Scan using twitter_test on users  (cost=0.43..60873.13 rows=51877 width=0) (actual time=279.184..293.532 rows=51833 loops=1)
        Filter: ((twitter)::text <> ''::text)
        Rows Removed by Filter: 2487830
        Heap Fetches: 26037
        Buffers: shared hit=51854 dirtied=19
Planning time: 0.191 ms
Execution time: 297.334 ms
```

