---
layout: post
title: Thế nào là một ứng dụng cloud native?
tags: [Design]
---

Cloud native là một thuật ngữ được dùng nhiều trong thời gian gần đây, ngay cả khách hàng của chúng tôi cũng yêu cầu thiết kế hệ thống cloud native.
Khi thực hiện xây dựng, thiết kế hệ thống chúng ta có thể thấy được rất nhiều lợi ích, những cloud native cũng mang lại những thách thức trong việc thiết kế,
triển khai hệ thống.

### 1. Cloud native là gì? Những trụ cột trong cloud native là gì?
Refer: [What is Cloud native?](https://cloud.google.com/learn/what-is-cloud-native#section-3)

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

Thông qua những trụ cột của Cloud Native, chúng ta có thể thấy rằng Cloud native dường như là một tập hợp những best practice để xây dựng ứng dụng trên cloud. Tuy nhiên Cloud Native không chỉ là như vậy. Vậy sự khác biệt khi ta nói đến Cloud và Cloud Native là gì?

Thực sự có sự khác biệt giữa Cloud và Cloud Native. Cloud đề cập đến Cloud Computing, các dịch vụ sẽ được triển khai trên hạ tầng Cloud. 
Tuy nhiên thuật ngữ “Cloud Native” không chỉ nói về việc áp dụng, triển khai ứng dụng trên cloud. Thay vào đó, nó đề cập đến cách các ứng dụng được xây dựng và phân phối chứ không chỉ là nơi chúng được triển khai. Trong một số trường hợp, ứng dụng thậm chí có thể không chạy trên Cloud.

### 2. Ứng dụng thiết kế theo Cloud Native như thế nào?
Trước khi microservice trở lên phổ biến. Khi xây dựng một ứng dụng chúng ta có có một kiến trúc cho ứng dụng như:

<img src="https://learn.microsoft.com/en-us/dotnet/architecture/cloud-native/media/monolithic-design.png" alt="architecture_1" width="500">

Bạn xây dựng một ứng dụng bao gồm tất cả domain logic, business. Các module đều được đóng gói trong một mã nguồn, các module đều chạy trên một máy chủ duy nhất. Các mô-đun chia sẻ một cơ sở dữ liệu quan hệ. Đó là mô hình tiêu biểu cho kiến trúc monolithic.

Thành thật mà nói, kiến trúc monolithic không phải lúc nào cũng tệ, đôi khi nó lại hoạt động tốt.

Rất nhiều ứng dụng ngày nay được tạo ra dựa trên kiến trúc monolithic. Ứng dụng sau đó tiếp tục phát triển, hết lần này đến lần khác, bổ sung thêm nhiều chức năng hơn. Tuy nhiên, đến một lúc nào đó, bạn bắt đầu cảm thấy khó chịu. Bạn thấy mình mất quyền kiểm soát ứng dụng. Thời gian trôi qua, việc mất kiểm soát càng ngày càng tồi tệ hơn và cuối cùng bạn bước vào trạng thái được gọi là Chu kỳ sợ hãi (Fear Cycle):

- Ứng dụng này đã trở nên cực kỳ phức tạp đến mức không một ai có thể hiểu được nó.
- Bạn sợ phải thay đổi - mỗi thay đổi đều có những tác dụng phụ không mong muốn và tốn kém.
- Các tính năng/bản sửa lỗi mới trở nên phức tạp, tốn thời gian và tốn kém khi triển khai.
- Mỗi bản phát hành trở nên nhỏ nhất có thể và yêu cầu triển khai đầy đủ toàn bộ ứng dụng.
- Một thành phần không ổn định có thể làm hỏng toàn bộ hệ thống.
- Các công nghệ mới không phải là một lựa chọn.
- Rất khó để triển khai các phương pháp triển khai, phát hành sản phẩm một cách nhanh chóng và đáng tin cậy.

Cuối cùng, các chuyên gia tư vấn đến và bảo bạn viết lại. Để giải quyết Fear Cycle, rất nhiều tổ chức chọn cách tiếp cận theo Cloud Native.
Khi ứng dụng ứng dụng cloud native, thì kiến trúc sẽ được thay đổi như dưới đây:

<img src="https://learn.microsoft.com/en-us/dotnet/architecture/cloud-native/media/cloud-native-design.png" width="500">

Nhìn qua kiến trúc trên thì cũng rất khó để nhận biết một ứng dụng Cloud native cần phải đảm bảo, và triển khai như thế nào? 
Tuy nhiên chúng ta có thể đánh giá một ứng dụng thông qua những yếu tố sau. Theo tài liệu của Ms thì chúng ta có 12 yếu tố. 
Refer: 

[Cloud Native Definition](https://learn.microsoft.com/en-us/dotnet/architecture/cloud-native/definition) và [12 yếu tố khi triển khai](https://12factor.net)

| Factor    | Explanation |
| -------- | ------- |
| 1 - Code Base  | A single code base for each microservice, stored in its own repository. Tracked with version control, it can deploy to multiple environments (QA, Staging, Production).   |
| 2 - Dependencies | Each microservice isolates and packages its own dependencies, embracing changes without impacting the entire system.    |
| 3 - Configurations    | Configuration information is moved out of the microservice and externalized through a configuration management tool outside of the code. The same deployment can propagate across environments with the correct configuration applied.   |
| 4 - Backing Services | Ancillary resources (data stores, caches, message brokers) should be exposed via an addressable URL. Doing so decouples the resource from the application, enabling it to be interchangeable. | 
|5 - Build, Release, Run | Each release must enforce a strict separation across the build, release, and run stages. Each should be tagged with a unique ID and support the ability to roll back. Modern CI/CD systems help fulfill this principle. | 

...

Chi tiết có thể xem ở link tham khảo phía trên. Tài liệu mô tả rất chi tiết về các factor.



