---
layout: post
title: Quick note về API idempotency
tags: [Design]
---

Khi nói về idempotency của API thì có khá nhiều bạn dev có thể hiểu tuy nhiên khi áp dụng vào thực tế design thì lại
có một số vấn đề, đó là áp dụng sai hoặc không nhận ra.

Chúng ta hãy bắt đầu bằng một api với yêu cầu như sau: 
Client sẽ gửi request bao gồm thông tin về User và OrderId, Server sẽ gửi lại kết quả đã được mã hóa bao gồm "Timestamp + UserId + OrderId". Sau đó chuỗi mã hóa này có thể được dùng để generate ra QR code.

Và điều gì xảy ra khi dev thiết kế API này với phương thức GET or POST. 
```
Solution1: 
- path: v1/api/order/qr-code
  method: GET

Solution2: 
- path: v1/api/order/qr-code
  method: POST
```

Sẽ có điểm tranh luận ở đây, khi thực hiện review design thì chúng ta sẽ nhận được comment là API này "v1/api/order/qr-code"không idempotent. Do đó cần sử dụng method POST.
Tại sao lại như vậy? Để trả lời câu hỏi này chúng ta hãy xem "idempotent API là gì?"

*What is  an idempotent API?*
Trong REST APIs thì một API được coi là idempotent khi mà api này được gọi N lần với request là giống nhau thì 
tác động ảnh hưởng, gây ra resouce là giống nhau và giống như việc api này được gọi 1 lần. Hay nói theo cách khác thì 
kết quả trả về của idempotent API là giống nhau. Điều này có ý nghĩa gì?
Khi thiết kế API chúng ta phải nhận thấy rằng rất có thể phía consumer có thể gặp lỗi khi họ sử dụng API.
Ví dụ như consumer có thể tạo ra duplicate lời gọi API, do đó nếu API là idempotent thì việc duplicate lời gọi sẽ không
có ảnh hưởng xấu tới hệ thống.

Quay trở lại bài toán qr-code phía trên thì rõ ràng sau mỗi lần gọi thì server sẽ trả lại kết quả là một chuồi mã hóa với thông tin timestamp khác nhau. Do đó API này không idempotent.



