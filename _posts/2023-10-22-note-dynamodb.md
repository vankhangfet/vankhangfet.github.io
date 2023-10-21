---
layout: post
title: Dynamo DB một số điều cần lưu ý
tags: [Design]
---

Dynamo DB là một NoSQL rất hay được sử dụng trên AWS. Bạn có thể sử dụng Dynamo trong hầu hết các ứng dụng. Nó rất đơn giản, và cho phép lưu trữ cũng như truy vấn 
với dữ liệu lớn rất tuyệt vời. Tuy nhiên khi thiết kế với Dynamo DB cũng không hề dễ dàng. Việc thiết kế cơ sở dữ liệu với Dynamo không dễ dàng như bạn nghĩ.
Hãy thử xem qua một số vấn đề khi làm việc với Dynamo, bạn đã bao giờ gặp vấn đề với Throttling? 

What is DynamoDB Throttling?
Như các bạn đã biết thì khi lưu trữ dữ liệu thì Dynamo gồm rất nhiều các "partion". Các bản ghi sẽ được lưu trữ trong các partion này.
Việc lưu dữ vào partion sẽ được lưu trữ dựa trên partion key.
