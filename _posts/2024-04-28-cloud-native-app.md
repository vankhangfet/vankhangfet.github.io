---
layout: post
title: Thế nào là một ứng dụng cloud native?
tags: [Design]
---

Cloud native là một thuật ngữ được dùng nhiều trong thời gian gần đây, ngay cả khách hàng của chúng tôi cũng yêu cầu thiết kế hệ thống cloud native.
Khi thực hiện xây dựng, thiết kế hệ thống chúng ta có thể thấy được rất nhiều lợi ích, những cloud native cũng mang lại những thách thức trong việc thiết kế,
triển khai hệ thống.

### 1. Cloud native là gì? Những trụ cột trong cloud native là gì?
Refer: https://cloud.google.com/learn/what-is-cloud-native#section-3

<img src="https://learn.microsoft.com/en-us/dotnet/architecture/cloud-native/media/cloud-native-foundational-pillars.png" alt="drawing" width="500"/>

#### 1.1 Microservices: 
Hầu hết tất cả kiến ​​trúc đám mây đều dựa trên kiến trúc microservices, nhưng lợi ích mà chúng mang lại là khả năng kết hợp—chia ứng dụng thành các dịch vụ nhỏ hơn, nhẹ hơn, có thể dễ dàng cấu thành và kết nối với nhau thông qua giao diện lập trình ứng dụng (API).

#### 1.2 Containers and orchestration:

Container chứa các component có thể thực thi được, gồm các thành phần cần thiết—bao gồm mã nguồn ứng dụng và các dependency để mã nguồn, chương trình có thể chạy được trong mọi môi trường. Khả năng cũng như ý tưởng của Container đó là “build once, run anywhere”, giúp việc phát triển và triển khai trở nên dễ dàng hơn đáng kể. Chúng cũng giúp giảm nguy cơ xung đột giữa các ngôn ngữ, thư viện và khung vì chúng có thể được triển khai độc lập. Tính di động và linh hoạt này làm cho các container trở nên lý tưởng để xây dựng kiến ​​trúc microservice.

Trong hệ thống phức tạp với nhiều services thì việc quản lý các Containers cũng rất cần thiết vì số lượng services càng tăng do đó để đảm bảo việc quản lý Containers dễ dàng chúng ta cần Containers Orchestration. Khi nhắc đến Container Orchestration thì Kubernetes là một công cụ rất hữu ích, với khả năng quản lý rất mạnh mẽ.

#### 1.3 DevOps:
Việc phát triển ứng dụng trên nền tảng Cloud yêu cầu phương pháp như DevOps, nơi các nhà phát triển và nhóm vận hành cộng tác để tự động hóa quy trình phân phối phần mềm và cơ sở hạ tầng. DevOps cho phép các nhóm phát triển và vận hành giao tiếp chặt chẽ hơn và cùng nhau hướng tới một mục đích chung, tạo ra văn hóa và môi trường nơi các ứng dụng có thể được xây dựng, thử nghiệm và phát hành nhanh hơn.

#### 1.4 Continuous integration and continuous delivery (CI/CD):
Quy trình CI/CD giúp tự động hóa quá trình xây dựng, thử nghiệm và triển khai các thay đổi của ứng dụng một cách nhanh chóng và tin cậy.
