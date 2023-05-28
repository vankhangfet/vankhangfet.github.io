---
layout: post
title: Các đặc tính ACID trong database là gì ? Tại sao các đặc tính này lại quan trọng?
tags: [SoftwareDesign]
---

Khi làm việc với Database chắc hẳn các bạn đã nghe thấy transaction. Nhưng không phải ai cũng hiểu rõ và nhớ đến ACID? 
Vậy ACID là gì? Đã có rất nhiều bài viết chi tiết về ACID rồi, mình có tóm gọn lại một số điểm chính sau. 
```
ACID transactions guarantee that a database will be in a consistent state after running a group of operations. 
Most databases offer transactional guarantees for operations that impact a single record. 
```
ACID transaction đảm bảo cho dữ liệu của bạn sẽ nhất quán, khi bạn thực hiện một nhóm các thao tác (insert/update/delete).
Thông thường các DB hiện nay luôn dảm bảo tính ACID cho các thao tác (insert/update/delete) trên một record. Tuy nhiên cũng có 
những DB sẽ đảm bảo điều nay trên nhiều record/document. 

