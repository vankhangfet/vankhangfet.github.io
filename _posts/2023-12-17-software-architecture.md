---
layout: post
title: Kiến trúc phần mểm là gì? Làm thế nào để có thể tạo nên một Clean Architecture
tags: [Design]
---

Quay trở lại cách đây 10 năm, khi tôi mới chập chững vào nghề. Lần đầu tiên khi tham gia vào tìm hiểu một dự án phần mềm, nhiệm vụ của tôi là cần tiếp tục phát triển 
phần mềm đó. Khi bắt đầu tìm hiểu, tôi có nhận được câu hỏi của anh trưởng nhóm quản lý kỹ sư: 

"Em hãy mô tả hay vẽ lại kiến trúc của phần mềm này? Ứng dụng này được xây dựng trên kiến trúc như thế nào vây?"

Vì thời gian trước đó, tôi chỉ tham gia vào viết code, và việc thiết kề là một nhiệm vụ mà tôi đã không hề biết đến. Tất nhiên tôi đã không trả lời được câu hỏi này.
Sau đó anh đưa cho tôi một số tài liệu để tham khảo? Theo tôi thì tài liệu của Micsoft là một trong những tài liệu rất hay để tham khảo.
Refer: https://learn.microsoft.com/en-us/previous-versions/msp-n-p/ee658093(v=pandp.10)


Và khi nhắc đến kiến trúc phầm mềm (software architecture) tôi hy vọng các bạn sẽ thấy không xa lạ, và tất nhiên để có thể phát triển một ứng dụng tốt, bạn cần hiểu 
rất rõ kiến trúc của ứng dụng đó. Vậy kiến trúc phần mềm là gì? Điều gì hay những thành phần nên được mô tả trong kiến trúc phần mềm?

Bạn có thấy hình vẽ dưới đây rất quen thuộc phải không? 

<img src="https://learn.microsoft.com/en-us/previous-versions/msp-n-p/images/ee658124.b8220f0d-f76a-40d6-8b1b-5279f7cdcee9(en-us,pandp.10).png" height="350">

Đây là một trong những kiến trúc rất phổ biến, và khi nhắc tới software architecture chúng ta sẽ đề cập đến vấn đề sau: 
- High-level 
- Structure 
- Layers 
- Components 
- Relationships

Tuy nhiên những mô tả trên chỉ nên dùng ở mức trừu tượng, và software architecture trừu tượng những gì?

- Layers
- Components
  
<img src="/assets/img/sa-01.png" height="300">

Khi hệ thống trở lên phức tạp thì kiến trúc phần mềm cũng phức tạp dần lên, và bắt đầu nảy sinh nhiểu vấn đề đó là *Messy vs Clean Architecture*

<img src="/assets/img/sa-02.png" height="300">

Nếu duy trì một kiến trúc tồi sẽ phát sinh rất nhiều vấn đề trong tương lai, nó sẽ gây tốn kém khi hệ thống có yêu cầu mới, cũng như làm giảm khả năng bảo trì.
Vậy làm thế nào để có thể tạo ra một Clean Architecture. Nhìn lại cách thiết kế, khi thiết kế chúng ta có hướng tiếp cận theo dữ liệu (data first) hay theo nghiệp vụ (domain)?
*Database- vs. Domain-centric*

Để dễ hình dung, chúng ta có thể xem ví dụ dưới đây. Điểm khác biệt giữa 2 cách tiệp cận, kiến trúc này đó là trung tâm (core). Thay vì tập trung ở vào những gì ở data layer, ta nên tập trung ở nghiệm vụ (domain)
<img src="/assets/img/sa-03.png" height="300">

Nhìn qua thì có vẻ khá đơn giản phải không? Nhưng không hề như vậy, Clean Architecture cũng có rất nhiều cách triển khai và góc nhìn khác nhau. Phổ biến là các kiểu kiến trúc sau:

- Hexagonal Architecture
  
<img src="/assets/img/sa-04.png" height="300">

- Onion Architecture
- Clean Architecture


