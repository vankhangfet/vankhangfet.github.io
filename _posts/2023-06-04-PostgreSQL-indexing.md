---
layout: post
title: Hiểu về index trong PostgreSQL?
tags: [SoftwareDesign]
---

Khi làm việc với DB, thực hiện các câu truy vấn chắc hẳn bạn đã từng sử dụng Index để tăng tốc query. Nhưng thật đáng tiếc là
không có nhiều bạn developer hiểu đúng và thực hiện đúng khi tạo Index. Chúng ta hãy tìm hiểu vấn đề kỹ hơn.

Mặc dù bài viết này chủ yếu là đề cập đến việc Indexing cho DB Postgre nhưng bạn có thể áp dụng cho bất kỳ SQL database khác.

Trước khi đi chi tiết hơn, chúng ta hãy xem một ví dụ đơn giản sau: 
Giả sử chúng ta thực hiện câu truy vấn trên một tập dữ liệu lớn với table có hàng triệu record và user.id là giá trị unique
```
SELECT * FROM users WHERE users.id = 'user411' LIMIT 1;
```
Điều gì sẽ xảy ra khi bạn thực hiện Index và chạy câu truy vấn trên

```
CREATE UNIQUE INDEX slug_idx ON users (slug);
```
Rõ ràng bạn thấy rằng tốc độ đã được cải thiện rất nhiều lần. Vậy thực sự Index là gì? Và tại sao nó giúp cải thiện tốc dộ tốt như vậy.

Giải thích ở mức high-level thì bạn có thể hình dung index trong một tình huống như sau. Việc tìm kiếm dữ liệu giốg như bạn thực hiện tra từ điển, khi tra từ điển thì trong cuốn từ điển, các từ vựng đã đã xếp lại theo thứ tự chữ cái. Do đó việc khoanh vùng tiếm kiếm sẽ dễ hơn. Nói tóm lại khi bạn tạo Index thì database giúp bạn tạo ra một cấu trúc dữ liệu đã được sắp xếp, từ đó việc tìm kiếm sẽ nhanh hơn.