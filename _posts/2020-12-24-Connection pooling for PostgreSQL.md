---
layout: post
title: Connection pool trong PostgreSQL
tags: [Others]
---

Khi làm việc với database, chúng ta sẽ gặp một số khải niệm như Connection pool. Post này chúng ta sẽ tìm hiểu xem connection pool là gì? 
Tại sao chúng ta cần quan tâm tới Connection Pooling. Cụ thể trong tình huống này là Connection Pooling trong Postgres. 

Connection pooling có thể xem là một phương pháp để tạo ra một pool gồm nhiều connection và những connection này sẽ được tái sử dụng.
PostgreSQL có một tiến trình "Postmaster", tiến trình này sẽ tạo ra các kết nối tới database. Tiến trình này sẽ dùng khoảng 2~3MB trong bộ nhớ, 
mỗi khi bạn khởi tạo một kết nối tới DB. Nếu như không dùng Connection Pool, với mỗi kết nối "Postmaster" sẽ sử dụng 2~3MB memory điều này dẫn đến 
vấn đề khi có quá nhiều connection tới DB sẽ tiêu tốn rất nhiều bộ nhớ một cách không cần thiết.

Khi sử dụng Connection Pool, khi service tạo kết nối với DB thì connection sẽ được lấy từ trong pool ra để sử dụng. Mỗi khi một session hoặc transaction kết thúc 
thì connection này sẽ được trả lại pool. 

Điều này sẽ giúp tăng hiệu năng? Đúng vậy khi sử dụng Connection Pool, khi có nhiều request khởi tạo connection đến cùng một DB, thì Connection Pool sẽ không khởi tạo
mới connection nữa. Connection Pool sẽ tái sử dụng những connection có trong Pool trước đó, do đó sẽ tránh được việc DB server phải giữ rất nhiều connection từ client 
khởi tạo tới. 

Nhưng thực tế thì PostgreSQL không dược build-in connection pooler, Client sẽ phải tạo ra và quản lý pool này. Có 2 cách để tạo ra Connection Pool

1. On the application side : Có rất nhiều framwork hỗ trợ việc khởi tạo và quản lý Connection Pool này. Do đó các bạn nên sử dụng những thư viện hay framework hỗ trợ
việc này.

2. External service : Service này sẽ đứng giữa Client và DB server. Client sẽ connect tới External service thay vì kết nối trực tiếp tới DB. Với PostgreSQL bạn nên dùng
Connection Pool rất phổ biến đó là PgBouncer.

OK! note này khá ngắn ngọn về Connection Pool, hy vong có thể giúp ích được các bạn.
