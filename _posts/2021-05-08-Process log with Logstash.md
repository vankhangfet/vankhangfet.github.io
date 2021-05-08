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
