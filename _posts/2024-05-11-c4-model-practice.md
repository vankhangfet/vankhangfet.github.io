---
layout: post
title: Thiết kế, mô tả hệ thống với C4 model.
tags: [Design]
---
Trong một meeting, tôi được anh bạn đồng nghiệp giới thiệu về dự án mà team anh sẽ tham gia phát triển. Qua cuộc họp,
tôi thấy rằng team phát triển đã hiểu được hệ thống và đang chuẩn trong quá trình thiết kế (Architecture Design, Detailed design, etc.).
Tuy nhiên cách trình bày hệ thống của đội phát triển không được tốt như tôi mong đợi, họ dùng quá nhiều slide để mô tả về hệ thống với chất lượng không tốt.
Tôi thấy rằng, để mô tả hệ thống đội phát triển có thể áp dụng C4 model, như vậy hệ chất lượng tài liệu sẽ tốt hơn và dễ dàng chia sẻ cập nhật.

C4 model là gì thì các bạn có thể xem tại https://c4model.com. Các thành phần, cũng như khái niệm rất dễ để hiểu và áp dụng. Về việc thiết kế tài liệu theo C4 mode
thì các bạn có thể dùng draw.io, tôi thấy đây là một công cụ rất dễ, thuận tiện để sử dụng.

Mô tả qua về hệ thống mà đội phát triển sẽ làm, đó là họ sẽ cần phải phát triển cũng như thực hiện kiểm thử một thuật toán điều khiển các thiết bị IoT trong phòng.
Các bạn có thể hình dung hệ thống như sau: Khi có sự thay đổi về nhiệt độ, ánh sáng hoặc một yếu tố nào đó thì thuật toán sẽ điều gửi tham số tới hệ thống điều khiển
để điều chỉnh thiết bị (điều hòa, bóng điện,etc.) và hệ thống này được thiết kế sử dụng AWS.

Vậy khi sử dụng C4 model, để mô tả về hệ thống này sẽ như thế nào? Vì tôi không thể vẽ qua chi tiết hệ thống nhưng tôi sẽ cố gắng mô tả hệ thống này gần bài toán 
của đội phát triển nhất có thể.

Chúng ta sẽ bắt đầu với System Context diagram, hệ thống sẽ được mô tả như sau:

<img src="/assets/img/Iot_alg_sys_context.png" width="450px">


