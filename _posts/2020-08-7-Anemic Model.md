---
layout: post
title: Anemic model
tags: [DDD]
---
Khi tìm hiểu về DDD thì mình có gặp bài viết về Anemic Model. Trong post này mình note lại một số điểm về Anemic model. 
1. Anemic model là gì? 
2. Những best practice mà chúng ta có thể sử dụng để tránh việc tạo ra những Anemic model. 

OK bắt đầu thôi.

1. Anemic model là một domain model khi mà domain object không có business logic hoặc có rất ít business logic.
Anemic model được mô tả lần đầu tiên bởi Martin Flower, và Anemic model là một antipattern. Tại sao nó lại là một anti-pattern 
" Anmic model đi ngược lại với ý tưởng cơ bản của hướng đối tượng đó (OOP - là sự kết hợp giữa data và process)"
~~~~
"The fundamental horror of this anti-pattern is that it’s so contrary to the basic idea of object-oriented design; 
which is to combine data and process together."

Martin Fowler, Anemic Domain Model, 2003
~~~~

Với Anemic model, thì client phải mô tả nhiệm vụ và cách sử dụng Domain object. Nhưng theo thiết kế việc này sẽ được đảm nhiệm, hay implement 
trong những class khác, hay còn gọi là Services.

2. Làm thế nào để hạn chế việc tạo ra những Anemic model 

- Cài đặt thuộc tính Private Setter.

- Entities phải self validate.

- Tránh việc tạo ra constructor mà không có tham số đầu vào.

- Thận trọng khi sử dụng những framwork ORM vì ORM sẽ tự động tạo ra những Domain Object và những Domain Object này sẽ có public setter --> Điều này có thể gây ra việc
tạo ra Anemic model
