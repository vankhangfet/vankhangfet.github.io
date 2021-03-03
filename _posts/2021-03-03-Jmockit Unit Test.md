---
layout: post
title: Unit Test - What are diffrences between @Mocked and @Injectable in JMockit
tags: [Unit Test]
---


Dự án trước chúng tôi có cơ hội làm việc với thư viện Jmockit để thực hiện viết Unit test. Về cảm nhận thì Jmockit khá đơn giản, dễ dùng.

Tuy nhiên có một số concept và từ khóa đôi khi gây khó hiểu đó là @Mocked và @Injectable. 

Trong mọi trường hợp thì @Mocked sẽ mock cho tất cả các instance của class đó, còn @Injectable sẽ chỉ mock cho cụ thể method / field. 

Theo kinh nghiệm thì chúng ta có thể tóm tắt @Mocked và @Injectable như dưới đây:

- @Injectable sẽ được dùng khi bạn có thể PASS instance mà mark @Injectable vào trong class bạn muốn test 

- @Mocked được dùng khi bạn không thể PASS instance mà mark @Mocked vào trong class bạn muốn test. 




