---
layout: post
title: Nên viết tài liệu design thế nào cho tốt?
tags: [SoftwareDesign]
---

Trong quá trình phát triển sản phẩm, chúng ta sẽ cần các tài liệu đặc tả cho hệ thống. Có thể kể đến những tài liệu sau
1. Architecture Design
2. Detailed Design 
3. Deployment 
4. etc. 

Khi hệ thống hay ứng dụng được phát triển trong một thời gian dài thì lượng tài liệu sẽ càng phức tạp, trở nên khó kiểm soát hơn.
Vậy chúng ta cần phải có một cách thức, phương pháp để quản lý tài liệu tốt hơn. Với xu hướng everything as code, chúng ta nên 
document bằng việc code. Cụ thể ở đây là tài liệu nên được viết bằng md file (https://www.markdownguide.org), seq nên được vẽ công cụ như PlantUml ( https://plantuml.com/class-diagram).
Ngoài ra khi viết tài liệu thiết kế cần chú ý những điểm sau:

1. Nên sử dụng từ ngữ mô tả hệ thống càng nhiều càng tốt, hạn chế sử dụng image.

2. Cần đặc tả Non functional REQ càng chi tiết càng tốt. Vì functional REQ là một yêu rõ ràng. Những yêu cầu về Non functional REQ thường 
mơ hồ và không rõ ràng tại thời điểm ban đầu.

3. Với những thành phần hay mô tả chi tiết cần mô tả thật rõ ràng và có tham chiếu chi tiết.

4. Nếu tài liệu hay mô tả hệ thống nhưng chưa ở mức thiết kế chi tiết thì nên sử dụng từ ngữ "abstraction".
