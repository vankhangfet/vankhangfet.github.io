---
layout: post
title: Những lập trình viên senior sẽ viết bao nhiêu dòng code mỗi ngày?
tags: [Others]
---

Thời gian vừa qua tôi có nhận được estimation của khá nhiều dự án, và một trong số đó dùng line of code để ước lượng ra effort để thực hiện.
Khi nhìn vào bảng tính tôi thấy rất nhiều con số, có những tính năng phát triển tương đối ngắn nhưng số lượng dòng code lại rất nhiều?. Tôi tự hỏi khi estimation thì sẽ dùng con số line of code như thế nào là hợp lý? Line of code là một metric rất quan trọng, nó có thể cung cấp cho bạn biết được độ phức tạp, cũng như effort để có thể hoàn thành tính năng,
ứng dụng đó.

Theo như mythical book [The Mythical Man-Month](https://en.wikipedia.org/wiki/The_Mythical_Man-Month) thì đối với lập trình viên cấp độ senior thì họ sẽ viết 10 line of code mỗi ngày, không phụ thuộc là ngôn ngữ nào. Nhưng để con số line of code có ý nghĩa có lẽ cần phải thống kê trên một dự án lớn và dài hơi, nếu dự án ngắn hạn thì con số có lẽ sẽ không
chính xác. Cụ Bill Gate cũng đã có comment: 
“Measuring software productivity by lines of code is like measuring progress on an airplane by how much it weighs.“.

Điều này có thể dễ nhận thấy là có ngày chúng ta có thể viết 200 LOC, nhưng có ngày lại chỉ có thể viết chỉ 10 LOC. Nhưng con số 10 LOC như trong cuốn sách đề cập có vẻ là một con
số hơi thấp, sau một thời gian tìm hiểu thì tôi đã thấy rằng con số 80 LOC/ per day là một con số khá hợp lý. 

Con số này đã được đo lường qua rất nhiều dự án, bạn có thể tìm hiểu chi tiết tại đây https://blog.ndepend.com/mythical-man-month-10-lines-per-developer-day/

80 LOC /per day là một con số tốt để duy trì tính ổn định của mã nguồn, cũng như năng suất của dự án.

