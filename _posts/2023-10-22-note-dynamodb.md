---
layout: post
title: Dynamo DB một số điều cần lưu ý
tags: [Design]
---

Dynamo DB là một NoSQL rất hay được sử dụng trên AWS. Bạn có thể sử dụng Dynamo trong hầu hết các ứng dụng. Nó rất đơn giản, và cho phép lưu trữ cũng như truy vấn 
với dữ liệu lớn rất tuyệt vời. Tuy nhiên khi thiết kế với Dynamo DB cũng không hề dễ dàng. Việc thiết kế cơ sở dữ liệu với Dynamo không dễ dàng như bạn nghĩ.
Hãy thử xem qua một số vấn đề khi làm việc với Dynamo, bạn đã bao giờ gặp vấn đề với Throttling? 

What is DynamoDB Throttling?
Như các bạn đã biết thì khi lưu trữ dữ liệu thì Dynamo gồm rất nhiều các "partition". Các bản ghi sẽ được lưu trữ trong các partion này.
Việc lưu dữ vào partion sẽ được lưu trữ dựa trên partition key. Ngoài ra thì mỗi partition có giới hạn tối đa read/write (RCUs/WCUs) là 3000 RCUs và 1000 WCUs. 
Nhưng cần lưu ý là giớ hạn này được chia đều cho các partions. Để cho dễ hiểu ta hãy xem ví dụ sau:
Giả sử chúng ta configure RCUs và WCUs là 50 cho table và tabel này có 2 partition thì mỗi partition sẽ có giới RCUs/WCUs là 25.

Do đó mỗi khi bạn thực hiện read/write data vào table thì request sẽ được thực hiện trên các partition và khi số lượng read/write vượt quá giới hạn thì exception
Throttling sẽ xảy ra. Mặc dù chúng ta thấy rằng Dynamo DB là fully-mananged service, nhưng khi thiết kế vấn đề Throttling nên cần được quan tâm. 

Chúng ta đã biết mỗi khi tạo một table, AWS sẽ cung cấp cho chúng ta 2 lựa chọn 
1. Provisioned model
2. On-demand model





