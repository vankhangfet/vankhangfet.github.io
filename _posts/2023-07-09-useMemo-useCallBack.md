---
layout: post
title: Understading useMemo and useCallBack
tags: [React]
---
Trong quá trình làm việc với các bạn dev React, tôi nhận thấy rằng trong React có rất nhiều bạn developer gặp vấn đề khi sử dụng useMemo và useCallBack. Post này tôi hy vọng có thể giúp bạn hiểu rõ hơn về useMemo và useCallBack.

Trước khi đi vào chi tiết, chúng ta nên chuẩn bị môi trường làm việc để có thể thực hành và chạy example code. Việc này sẽ giúp các bạn hiểu hơn. Nếu bạn nào chưa có tài khoản trên codesanbox thì hãy đăng ký tại https://codesandbox.io

**Hãy bắt đầu với useMemo**

Ý tưởng của useMemo đó là lưu lại giá trị, trạng thái của ứng dụng trong mỗi lần render. Mặc dù React đã tối ưu việc re-render UI, nhưng React cung cấp thêm useMemo giúp các bạn tối ưu hơn nữa việc render:
 1. Giảm workload (số lượng task cần thiết cho việc render) khi cần thực hiện việc render.
 2. Giảm thời gian khi cần render lại component.

 Không có gì dễ hiểu hơn là show code: 
 
 **Use Case 1: Heavy computations**


