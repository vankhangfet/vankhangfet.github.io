---
layout: post
title: Nên mô tả hay report một issue thế nào để issue thực sự là issue?
tags: [Others]
---
Thời gian gần đây chúng tôi đã review và nhận thấy có một số vấn đề cần phải cải thiện, tối ưu trong hệ thống. Để mọi
việc có thể được quản lý, chúng tôi sẽ tiến hành log/tracking lại trên redmine or jira. Sẽ không có vấn đề gì xảy ra,
nếu như bạn là người log và trực tiếp xử lý issue đó. Vấn đề sẽ là khi một team member của bạn review hay đọc report về
issue này, reviewer hay người khác có thể không hiểu được issue của bạn là gì? Lúc này issue không rõ ràng hoặc không thực sự là
issue? Vậy làm thế nào để có thể mô tả một issue để mọi thành viên đều có thể issue và issue thực sự là issue? 
Mình suggestion các bạn hay mô tả theo theo trình tự như dưới đây 

Thông thường một report tốt sẽ bao gồm các hạng mục sau:
```
[1. Background]

[2. Issue]

[3. Solution] (Optinal)
```


[1. Background]
Dây chính là môt tả câu chuyện, xuất phát của vấn đề. Bạn nên mô tả để những người liên quan có thể hiểu rõ tình huống hoàn cảnh
của vấn đề, bussiness.

[2. Issue]
Để Issue thực sự là issue thì chúng ta nên mô tả ảnh hưởng của vấn đề, khi ảnh hưởng càng nhiều và càng chi tiết thì chúng ta sẽ 
có cái nhìn về issue rõ ràng hơn. Khi đó các action tiếp theo sẽ chính xác và hiệu quả hơn, nó giúp cho đội phát triển đưa ra 
các quyết định hữu ích. Vậy issue nên tập trung vào những gì? 

2.1 Hãy xem xét, đánh giá xem issue có ảnh hưởng gì tới end-user (User view point).

2.2 Sau đó tiếp tục đánh giá xem issue có ảnh gì tới hệ thống (System)?

2.3 Cuối cùng là ảnh hưởng tới đội phát triển (source code)? 

Khi chúng ta dùng 3 góc nhìn như vậy, chúng ta sẽ có cái nhìn toàn diện về mức độ ảnh hưởng.

[3. Solution] 

Đây là hạng mục cuối cùng, tuy nhiên hạng mục này sẽ được đưa ra khi chúng ta liệt kê hay đánh giá mức độ ảnh hưởng của vấn đề.

