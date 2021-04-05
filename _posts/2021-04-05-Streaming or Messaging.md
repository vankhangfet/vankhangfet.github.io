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

như ở ví dụ trên thì message có thể được thay thế bằng event. Tuy nhiên message và event sẽ có mục đích sử dụng khác nhau, các bạn có thể xem pattern CQRS để thấy
rõ sự khác nhau giữa chúng Command message (message) and Event message (event).

What is Streaming?

- Streaming of Data:  là luồng sự kiện liên tục trong đó mỗi sự kiện phải chứa đủ thông tin để phản ánh sự thay đổi trạng thái.
Nó cho phép quá trình xử lý dữ liệu diễn ra trong thời gian thực. Với stream chúng ta có ví dụ sau đây để phản ánh dòng dữ liệu.

Trong hệ thống chứng khoán. Mỗi khi có sự thay đổi về giá (stock price change), một sự kiện sẽ được tạo ra bao gồm thời gian,mã định danh cổ phiếu và giá giao dịch
mới của nó mà trong ví dụ này là sự thay đổi trạng thái. Do có hàng nghìn cổ phiếu và hàng nghìn giao dịch diễn ra mỗi giây, điều này dẫn đến một luồng dữ liệu liên tục


