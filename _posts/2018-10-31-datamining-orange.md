---
layout: post
title: Machine learning with Orange
image: /image/Orange_2.jpg
---
Orange là một công cụ khá trực quan để nghiên cưu về các thuật toán machine learning và thực hành data mining. Chi tiết về tool này các bạn có thể
xem ở trang web sau: (https://orange.biolab.si/), còn đây là quảng cáo trên site .
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
