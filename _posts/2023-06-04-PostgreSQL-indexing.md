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

**High-level definition**

Giải thích ở mức high-level thì bạn có thể hình dung index trong một tình huống như sau. Việc tìm kiếm dữ liệu giốg như bạn thực hiện tra từ điển, khi tra từ điển thì trong cuốn từ điển, các từ vựng đã đã xếp lại theo thứ tự chữ cái. Do đó việc khoanh vùng tiếm kiếm sẽ dễ hơn. Nói tóm lại khi bạn tạo Index thì database giúp bạn tạo ra một cấu trúc dữ liệu đã được sắp xếp, từ đó việc tìm kiếm sẽ nhanh hơn.

**Low-level definition**

Về chi tiết, sẽ có nhiều kiểu Index khác nhau. Một trong những kiểu dữ liệu phổ biến nhất là B-tree.
B-tree là một cây tìm kiếm cân bằng. Quay trở lại với bài toán tìm kiếm trong danh bạ, chúng ta có thể hình dung B-tree như sau: 

![Btree_contacts](/img/B-tree.png "B-tree contacts")

Tuy nhiên thực tế thì có nhiều kiểu Index, vơi mỗi kiểu index sẽ được thiết kế tối ưu cho những use-case khác nhau:

**B-tree** - the default index, 

Sẽ phù hợp với những toán tử truy vấn sau: <, <=, =, >=,>, BETWEEN, IN, IS NULL or IS NOT NULL

**Hash**

Kiểu Hash sẽ hoạt động rất tốt với toán tử  =


**GiST** 
- the shortcut that stands for Generalized Search Tree. Phù hợp với các toán tử sau: <<, &<, &>, >>, <<|, &<|, |&>, |>>, @>, <@, ~= or &&

**Khi nào cần Index?**

- Index columns that you search on
- Index columns used for join operations 
- Index column that you often use for sorting
