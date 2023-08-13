---
layout: post
title: Quick note về API idempotency
tags: [Design]
---

Khi nói về idempotency của API thì có khá nhiều bạn dev có thể hiểu tuy nhiên khi áp dụng vào thực tế design thì lại
có một số vấn đề, đó là áp dụng sai hoặc không nhận ra.

Chúng ta hãy bắt đầu bằng một api với yêu cầu như sau: 
Client sẽ gửi request bao gồm thông tin về User và OrderId, Server sẽ gửi lại kết quả đã được mã hóa bao gồm "Timestamp + UserId + OrderId". Sau đó chuỗi mã hóa này có thể được dùng để generate ra QR code.


