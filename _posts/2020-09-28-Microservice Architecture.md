---
layout: post
title: Kiến trúc Microservice
tags: [DDD]
---
Trong thực tế khi bạn phát triển một hệ thống enterprise application, thì hệ thống này phải đáp ứng rất, cung cấp nhiều những phiên bản API cho các ứng dụng khác nhau từ 
Desktop application, web application cho đến mobile application. Trong quá trình phát triển, hệ thống đòi hỏi khả năng mở rộng, cũng như mainteance cao do đó chúng ta cần một
kiến trúc tốt cho hệ thống này. Thì Micorservice là một trong những kiến trúc (pattern) tốt để xem xét khi xây dựng hệ thống.

Khi sử dụng kiến trúc Ms chúng ta sẽ thấy lợi ích sử dụng: 
1. Khi team bạn có rất nhiều devs với những stack công nghệ khác nhau.

2. Hệ thông sẽ dễ dàng với new member hơn.

3. Khi sửa chữa hệ thống sẽ trở lên dễ dàng và nhanh hơn. 

4. Team của bạn sẽ dễ dàng ứng dụng, hay thực hành CD trong quá trình phát triển. 

5. Với Ms việc bạn thử nghiệm, hay phát triển bằng những frame work hay công nghệ mới cũng sẽ dễ dàng hơn.

Đó là những lợi ích nhìn thấy khá rõ ràng khi apply kiến trúc Microservice. 

Tuy nhiên để tiếp hay xây dựng hệ thống theo Ms chúng ta cần tiếp cận như sau: 

1. Ứng dụng hay service phải có khả năng test (testable), bảo trì dễ dàng. Điều này cho phép chúng ta đẩy nhanh quá trinh phát triển, cũng như triển khai.

2. Các service phải có tính độc lập cao: điều này cho phép chúng ta phát triển các service một cách độc lập, không phụ thuộc lẫn nhau.

3. Services sẽ độc lập nhau trong quá trình deploy. Nghĩa là các service có thể deploy mà không cần phụ thuộc đền các service khác.

4. Việc phát triển các service nên được phụ trách bởi các team nhỏ, tránh việc dùng quá nhiều members chỉ để phát triển một service.

ngoài ra chúng ta cần xác định giao thức hay cách các service có thể giao tiếp được với nhau. Service có thế giao tiếp với nhau bằng cách sử dụng phương 
thức đồng bộ (synchronous) như HTTP/REST hay bất đồng bộ như AMQP. Các service có sử dụng riêng database để tránh việc phụ thuộc lẫn nhau.

[https://microservices.io/i/Microservice_Architecture.png](https://microservices.io/i/Microservice_Architecture.png) 

