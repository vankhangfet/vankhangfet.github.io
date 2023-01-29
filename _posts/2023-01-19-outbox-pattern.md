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
Ý tưởng của outbox pattern là thay vì việc ghi trạng thái vào database, sau đó public mesage vào trong queue được thực hiện ở các bươc khác nhau thì chúng ta sẽ lấy trạng thái từ DB sau đó thực hiện việc public message vào trong queue. State trong DB sẽ được delete/update khi và chỉ khi việc public message vào trong queue được thực hiện thành công. Tuy nhiên khi sử dụng outbox pattern đó chính là đặc tính "At least once", điêu này sẽ xảy ra khi việc delete/update lại database không thành công, dân đên việc publisher sẽ pooling lại message tư DB. 

Message được publish, hay state đươc lưu trữ trong cùng DB
![outbox04](/img/outbox_4.png "outbox4")

Sau khi state được lưu trữ trong DB thì, publisher sẽ pull từ trong DB để publish message vào trong queue

![outbox05](/img/outbox_5.png "outbox5")

Message được publish vào trong message broker
![outbox06](/img/outbox_6.png "outbox6")

Nếu như message được publish thành công, publisher sẽ delete/update lại trạng thái trong DB
![outbox07](/img/outbox_7.png "outbox7")

Do state luôn được lưu giữ trong DB, nên dù publisher không thực hiện được việc publish message vào trong queue thì chúng ta vẫn có thể thực hiện việc 
publish lại message.

Khi triển khai outbox pattern chúng ta tránh được việc mất mát message nhưng cần lưu ý vấn đề xử lý message tại consumer khi mà message sẽ là "At least once", nghĩa là việc message được gửi lại, hay lặp lại là có thể xảy ra.

Bài viết đươc tóm tắt lại từ 
https://codeopinion.com/outbox-pattern-reliably-save-state-publish-events/

