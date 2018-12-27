---
layout: post
title: Quick note về Hadoop và Bigdata
tags: [Bigdata]
---

Gần đây mình có tìm hiểu về Hadoop và bigdata, nên post này sẽ là những ghi chép nhanh về Hadoop và Bigdata.

Khi nhắc đến Bigdata thì người ta sẽ nghĩ đến dữ liệu lớn, vậy thì dữ liệu như thế nào thì được coi là bigdata.

## 1. Các định nghĩa về Big data 

Trên internet có rất nhiều dữ liệu bao gồm hình ảnh, video, âm thanh, văn bản,... Để dịnh nghìa là dữ liệu lớn thì người ta quan tâm đến
3 đặc tính của dữ liệu sau:

1. Volume: Kích cỡ của dữ liệu 
2. Velocity: tốc độ sinh ra của dữ liệu
3. Variety: Sự đa dạng về định dạng của dữ liệu 

Tuy nhiên gần đây, chúng ta còn quan tâm tới 3 đặc tính nữa của dữ liệu lớn. Đó là mô hình 6V, mơ rộng của 3V

4. Valuae: Giá trị của dữ liệu
5. Veracity: Chất lượng của dữ liệu
6. Viability: outcome prediction. 

Ngoài ra khi nhắc đến dữ liệu lớn thì đó là những dữ liệu không thể xử lý, hay lưu trữ bằng các hệ thống thông thường. Đó là lý do mà chúng ta phải sử dụng Hadoop để lưu trữ và xử lý dữ liệu.

## 2. Hadoop 

Ý tưởng của Hadoop là chia nhỏ dữ liệu, sau đó lưu trữ trên nhiều node khác nhau (máy tính khác nhau). Cấu trúc của Hadoop cũng dễ dàng đáp ứng cho việc truy vấn, lưu trữ dữ liệu. Thành phần chính trong Hadoop đó là HDFS và Map-Reduce.

2.1 HDFS (Hadoop Distributed File System)

2.2 Map - Reduce 
