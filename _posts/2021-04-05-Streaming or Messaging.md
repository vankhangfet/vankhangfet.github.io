---
layout: post
title: Lựa chọn Event Streaming hay Messaging khi thiết kế hệ thống?
tags: [DESIGN]
---

Trước khi đi vào việc lựa chọn thiết kế hệ thống với Streaming hay Messaging, chúng ta cần nắm rõ các khái niệm sau: 

What is an Event?

- Event miêu tả điều gì đã thay đổi, xảy ra. Hay nói cách khác nó bao gồm sự thay đổi của state trong ứng dụng. 
- Event phải nhỏ gọn và mang đủ thông tin để miêu tả sự thay đổi của state.
- Event được truyền tải thông qua các thành phần như streaming, messaging. 

Trong thực tế event xuất hiện ở khắp mọi nơi, ví dụ khi customer thuê một cuốn sách ở thư viện, thì trạng thái của cuốn sách đó sẽ chuyển từ 
"cho mượn" -> "đã được cho mượn"

What is a Message?

Khác với Event, Message cho ta biết được mục đích của action, mô tả điều gì đã xảy ra. Message có thể bao gồm nhiều thông tin. 
Message có thể được biến đổi, để phù hợp với các hệ thống khác nhau. Và tất nhiên message được phân phối thông qua các kênh Messaging. 

Qua định nghĩa trên thì ta thấy rằng Message và Event cũng có điểm chung. Vậy chúng có thể thay thế, hoán đổi cho nhau được không? 

Hãy xem ví dụ sau:


![No-DI](https://i1.wp.com/robertleggett.blog/wp-content/uploads/2020/03/Sample-Command-and-Event-Flow-Diagram.png?resize=768%2C747&ssl=1 "Event")
