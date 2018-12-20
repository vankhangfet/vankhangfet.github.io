---
layout: post
title: Độ phức tạp thuật toán.
tags: [Algorithm]
---

Độ phức tạp thuật toán là một phần rất thú vị, nhưng hầu hết anh em dev sau một thời gian sẽ không còn nhớ hoặc quan tâm đến nó nữa. Lý do là vì công việc, khi không dùng đến nữa thì sẽ quên mất. Post này mình cũng ôn lại một số kiến thức cơ bản, chỉ note lại những điểm cần nhớ thôi. 

## 1. Tính độ phức tạp thuật toán như thế nào?
Có một số quy tắc cơ bản cần nhớ như sau:

 1.1 Quy tắc bỏ hằng số: 
 Nếu chương trình P có thời gian thực hiện T(n) = O(c1.f(n)), thì có thể coi chương trình có độ phức tạp O(f(n)).
 
 1.2 Quy tắc cộng lấy max
 Nếu T1(n) và T2(n) là thời gian chạy của 2 chương trình P1 và P2. T1(n) = O(f(n)) và T2 = O(g(n)), thì độ phực tạp của 2 chương trình khi  gọi nối tiếp nhau sẽ là O(max(f(n),f(n))
 
 Ví dụ cho các bạn dễ hiểu, nếu như chương trình có phép gán x:=1 có độ phức tạp O(1) và sau đó là readln(x) có độ phức tạp là O(1).
 Khi đó độ phức tạp của cả chương trình sẽ là O(max(1,1))
 
 1.3 Quy tắc nhân 
  Nếu T1(n) và T2(n) là thời gian chạy của 2 chương trình P1 và P2. T1(n) = O(f(n)) và T2 = G(f(n)), thì độ phực tạp của 2 chương trình khi lồng  nhau sẽ là O(f(n) * g(n))
 
 
