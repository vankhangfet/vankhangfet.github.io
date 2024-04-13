---
layout: post
title: Sự khác nhau giữa Entities và DTOs
tags: [Design]
---
Chắc hẳn rất nhiều bạn đã quen thuộc với những thuật ngữ như Entity, DTO tuy nhiên tôi cũng nhận thấy có nhiều bạn chưa thực sự hiểu và nắm rõ những khái niệm này.
Entity và DTO chúng ta sẽ gặp rất nhiều trong các mã nguồn trong dự án hiện nay, việc chia tách hay định nghĩa các thành phần này sẽ làm cho mã nguồn có nhiều lợi ích.

### 1. Overview
   
Trong các dự án thực tế thì vai trò của Entity và DTO được phân chia rất rõ ràng, việc hiểu và tổ chức 2 thành phần này sẽ giúp cho mã nguồn tốt hơn, dễ bảo trì hơn.

### 2. Entity là gì?

Chúng ta nên hiểu Entity sẽ phản ảnh hay đại diện thực thể trong ứng dụng, hoặc thế giới thực. Ví dụ trong ứng dụng của chúng ta có Book, và trong mã nguồn chúng ta có thể 
nghĩ tới việc cần phải thiết kế một Entity là Book, vậy Entity Book này nên có những thuộc tính gì? Tất nhiên trong thực tế Book sẽ có tiêu đề, tác giả, giá bán,etc. Vậy nên
Entity cũng nên phản ánh hay có những thuộc tính như vậy. Tuy nhiên khi nhắc tới mã nguồn thì Entity sẽ có tương ứng trực tiếp với các bảng cơ sở dữ liệu hoặc các đối tượng lĩnh vực. Do đó, mục đích chính của chúng (Entity) là đóng gói và quản lý trạng thái và hành vi của các đối tượng này.

### 3. DTO
DTOs đúng như tên gọi chúng có nhiệm vụ chuyển dữ liệu, không có bất kỳ logic nào được triển khai trong. Chúng được sử dụng để truyền dữ liệu giữa các ứng dụng khác nhau hoặc các phần của cùng một ứng dụng.

Trong các ứng dụng đơn giản, việc sử dụng trực tiếp các Domain Object (Entity) vực như là DTO là phổ biến. Tuy nhiên, khi ứng dụng phức tạp hơn, việc tiết lộ toàn bộ Entỉy ra bên ngoài là không tốt nếu đánh giá từ quan điểm bảo mật và tính đóng gói.

