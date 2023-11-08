---
layout: post
title: CloudWatch một công cụ để phân tích log rất hữu dụng
tags: [Design]
---

Chắc hẳn khi xây dựng ứng dụng trên AWS thì bạn sẽ thấy việc lưu trữ quản lý log của ứng dụng là rất quan trọng. Từ log của application các bạn
có thể biết được ứng dụng của mình hoạt động ra sao, nếu phân tích log một cách kỹ càng chúng ta có thể thu được rất nhiều metric.
Để thành thục truy vấn, và lấy được những metric cần thiết thì bạn có thể tham khảo tài liệu của AWS về CloudWatch như sau:
https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/CWL_QuerySyntax-examples.html

Trong link chứa rất nhiều mẫu truy vấn cần thiết cho công việc của các bạn. Đã có bao giờ bạn cần phải trả lời câu hỏi "Trong 1s thì có bao nhiều reqs được gửi tới lambda hay 
web api của bạn?", hay trong 3 tháng gần nhất thì số lượng reqs lớn nhất trong 1s được gửi tới service của bạn là bao nhiểu?
Nếu như phải phân tích log mà không dùng Cloudwatch thì việc trả lời cho metric trên không hề dễ dàng. Nhưng với Cloudwatch log, va công cụ Logs Insights sẽ giúp bạn giải quyết
bài toán rất dễ dàng. Một trong những câu lệnh mình thấy khá hay đó là bin(). Hãy xem ví dụ sau: 

- Làm thế nào để biết có bao nhiều exception xảy ra trong vòng 1h với thời gian log cần thống kế là 3 tháng gần nhất? Các bạn hãy xem câu lệnh dưới đây:
````
filter @message like /Exception/ 
    | stats count(*) as exceptionCount by bin(1h)
    | sort exceptionCount desc
````
Câu lệnh này sẽ count các exception trong vòng 1h, còn thời gian thống kê là 3 tháng bạn chỉ cần chọn khoảng thời gian thống kê trên giao diện là được.
Còn rất nhiều những metric khác mà nếu như sử dụng CloudWatch cung cấp cho ta cách thức query. Hãy sử dụng CloudWatch nhiều nhất có thể.

