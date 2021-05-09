---
layout: post
title: Xử lý log với Logstash
tags: [DESIGN]
---

Dự án gần đây mình có cơ hội làm việc với rất nhiều công cụ xử lý event log. Logstash là một công cụ rất mạnh mẽ trong việc thu thập log và xử lý event log. 
Post này nhằm mục đích ghi lại quá trình tìm hiểu Logstash cũng như cách tương tác với Logstash để xử lý log. 

Backgound: 
Như các bạn đã biết trong hệ thống IoT thì việc tracing, hay log rất quan trọng. Khối lượng log là rất lớn, chúng ta cần theo dõi, kiểm tra hệ thống dựa trên
event log của hệ thống để có thể đưa ra các cảnh báo kịp thời.

Approach: 

Về hạ tầng hệ thống được xây dựng trên AWS, nên toàn bộ log, metric của các component sẽ được store trong cloudwatch. Chúng ta sẽ dùng Logstash để kết nối với 
cloudwatch, sau đo xử lý log và stogare với ElasticSeach. 

Hệ thống cơ bản của chúng ta sẽ có kiến trúc như sau: 

![Log pipelines](/img/Logging-Pipelines.png "Log Pipelines")
