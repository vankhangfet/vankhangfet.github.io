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

- Một file được chia thành mỗi block 64Mb. Các block này được lưu trữ trên các node khác nhau trong cluster. Trên mỗi node có một phần mềm để quản lý thông tin về các khối dữ liệu gọi là Data Node. 

- Các khối được lưu trữ nằm rải rác trong các node, thông tin "metadata" lưu trữ trên một máy gọi là Name Node.

- Mỗi block được tạo ra các bản sao và lưu trên 3 nodes khác nhau để đảm bảo khả năng recovery, sửa lỗi.

2.2 Map - Reduce 

Map-Reduce là một cách xử lý dữ liệu hiệu quả, ý tưởng đó là khi dữ liệu được chia thành nhiều phần nhỏ cho các Mapper và Reduce để chạy
trên các node. Việc xử lý dữ liệu sẽ có 2 phase chính Map -> Reduce.

Hãy xem ví dụ sau để hình dung về Map - Reduce. Mình có đọc trên blog của một bạn, lấy ví dụ về đếm tiền rất hay như sau:

Giả sử chúng ta có 99 bọc tiền gồm các loại tiền VND, USD, JPY nhiệm vụ của bạn là tính tổng mỗi loại tiền là bao nhiêu? Thời hạn có thời gian rất ngắn. Nếu tự mình đếm thì sẽ rất khó, bạn nảy ra ý tưởng nhờ 33 bạn để mở bao tải tiền để phân loại thành 3 cột. 1 Cột là USD, 1 cột là VND, 1 cột là JPY. Tiếp theo bạn nhờ 3 bạn để đếm tổng số ở mỗi cột. Như vậy để biết có bao nhiều tiền, chỉ cần hỏi 3 bạn đó là xong.

Trong Hadoop thì việc này được hiểu như sau:

- 99 bao tải tiền : Big data 
- Mỗi bao tải : block dữ liệu
- Nhóm 33 người: Mapper 
- Nhóm 3 người: Reducer 










