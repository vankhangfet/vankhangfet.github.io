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

Để hình dung dễ hơn về ACID chúng ta hãy xem ví dụ sau: 

```
Bạn thực hiện một function có chức năng cho phép userA --> chuyển tiền cho userB. Giả sử userA có tk và số tiền hợp lệ. Trình giao dịch được thực hiện sẽ như sau: 
1. Update số tiền trong tk userB.
2. Cập nhật số tiền trong tk userA.
3. ghi lại thông tin giao dịch với thông tin userA.
```
Điều gì xảy nếu 1 trong 3 giao dịch kia không thực hiện được? hoặc 1 in 3 fail? Chúng ta sẽ gặp vấn đề với Accouting,etc.
ACID sẽ đảm bảo giao dịch được an toàn và dữ liệu có tính thống nhất toàn vẹn.

A - Atomicity

C - Consistency 

I - Isolation

D - Durability

Tóm lại, hiểu về ACID là cần thiết, và ACID cung cấp cho dev cách thức thực hiện hay biết được rằng dữ liệu sẽ được toàn vẹn,
thống nhất khi thực hiện các thao tác trên dữ liệu.

