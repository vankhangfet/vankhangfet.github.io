---
layout: post
title: Outbox Pattern(phương thức thiết kế để lưu trạng thái và publish event đáng tin cậy)
tags: [Messaging]
---

# Outbox Pattern: Reliably Save State & Publish Events

# 1. What is outbox pattern: 
Đây là một mẫu thiết kế đảm bảo độ tin cậy khi bạn cần lưu trữ trạng thái vào trong database và publish message tới message broker. 
Pattern này giải quyết vấn đề gì? Bài toán đặt ra là khi bạn cần lưu trữ dữ liệu vào DB và sau đó push message vào message broker. Tuy nhiên database 
và message broker là 2 datasource khác nhau, như vậy để đảm bảo độ tin câỵ, chúng ta cần một distribution transaction để đảm bảo điều này. Outbox pattern sẽ giải quyết vấn đề này.

Để hiểu rõ hơn, hãy xem bài toán sau: 

Sự thay đổi (state) sẽ được lưu lại trong DB
![outbox01](/img/outbox_01.png "outbox1")

Sau khi dữ liệu được ghi trong DB thì hệ thống publish message vào message queue.
![outbox02](/img/outbox_02.png "outbox2")
Nhưng điều gì xảy ra khi việc public message vào trong queue không thực hiện thành công (failed)
![outbox03](/img/outbox_03.png "outbox2")
Nếu hệ thống của bạn đang thiết kế theo kiến trúc Event-Driven thì việc mất mát message sẽ gây ra rất nhiều vấn đề, và chúng ta cần tránh việc này xảy ra.

# 2. Outbox Pattern
Ý tưởng của outbox pattern là thay vì việc ghi trạng thái vào database, sau đó public mesage vào trong queue được thực hiện ở các bươc khác nhau thì chúng ta sẽ lấy trạng thái từ DB sau đó thực hiện việc public message vào trong queue. State trong DB sẽ được delete/update khi và chỉ khi việc public message vào trong queue được thực hiện thành công.
