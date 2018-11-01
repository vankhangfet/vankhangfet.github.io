---
layout: post
title: Machine learning with Orange
image:/img/Orange_1.jpg
tags: [Machine learning]
---
Orange là một công cụ khá trực quan để nghiên cưu về các thuật toán machine learning và thực hành data mining. Chi tiết về tool này các bạn có thể
xem ở trang web sau: [Orange.biolab.si](https://orange.biolab.si) , còn đây là quảng cáo trên site .
"Open source machine learning and data visualization for novice and expert. Interactive data analysis workflows with a large toolbox."
Bài này tôi sẽ trình bày qua về công cụ Orange này.

Khi khởi động chương trình xong, thì chương trình có giao diện như hình dưới:

Phía bên trái là các công cụ được chia làm nhiều nhóm khác nhau như

1. Data
2. Visualize
3. Model
4. Evaluate
5. Unsupervised

Các bước 1 ~4 cũng chính là các steps để chúng ta xây dựng nên một chương trình dùng machine learning.
Chi tiết các nhóm 1 ~ 4 ra sao, hy vọng các bạn sẽ tự tìm hiểu và bổ xung vào một bài viết khác.

OK! Để xem tool này ra sao ta sẽ xây dựng một flow như sau:

![Orange_1](/img/Orange_1.jpg "Orange_1")

Ví dụ ở workflow trên là bài toán phân loại hoa Iris dựa vào đặc điểm của chiều dài, rộng của cánh hoa,...
Các bước thực hiện như sau:

Step1: Load data set, ta sử dụng công cụ Data như sau:

![Orange_2](/img/Orange_2.jpg "Orange_2")

Tốt nhất ta nên chuẩn bị dataset dưới định dạng csv.

Step2: Chúng ta định nghĩa target. Ở đây ta cần phân loại ra loài hoa, nên chọn cột varity

![Orange_3](/img/Orange_3.jpg "Orange_3")

Step3: Tiếp theo ta cần lựa chọn thuật toán để build model. Ở đây mình chọn SVM (Support vector machine). Việc lựa chọn
thuật toán machine learning phụ thuộc vào bài toán của bạn, cũng như dữ liệu mà bạn có. Muốn thay đổi thông số của SVM
ta click vào icon SVM trên workflow.

![Orange_4](/img/Orange_4.jpg "Orange_4")

Step4: Sau khi đã có thuật toán, ta cần đánh giá model. Orange hỗ trợ rất nhiều phương pháp để đánh giá model như
Confusion matrix, ROC,... Chúng ta chỉ việc lựa chọn và kết nối theo hình vẽ dưới đây.

![Orange_5](/img/Orange_5.jpg "Orange_5")

Để xem kết quả, click và các icon tương ứng, dưới đây là một ví dụ về confusion matrix:

![Orange_6](/img/Orange_6.jpg "Orange_6")

Như vậy là ta đã xây dựng gần như hoàn chỉnh một workflow cho ứng dụng machine learning.
Orange là tool rất mạnh để trực quan và đánh giá nhan thuật toán machine learning, rất đáng để thử trong các dự án data mining, machine learning.

