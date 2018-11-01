---
layout: post
title: Sử dụng Open CV với C#
tags: [.Net]
---
Nếu bạn đã từng làm một số project có liên quan đến xử lý ảnh thì chắc hẳn sẽ biết thư viện OpenCV. Hiện tại đã có phiên bản OpenCV cho .Net là EmgCV, tuy nhiên với ứng dụng thương mại bạn sẽ phải trả tiền. Để tăng tốc độ xử lý cũng như dễ dàng hơn thì theo mình bạn nên sử dụng OpenCV trước sau đó mới đến EmguCV.

Với những ai chưa nghe đến OpenCV hoặc EmguCV bao giờ thì bạn có thể tham khảo ở link sau:
Open CV https://opencv.org (https://opencv.org)
EMGU CV http://www.emgu.com/wiki/index.php/Main_Page (http://www.emgu.com/wiki/index.php/Main_Page)

OpenCV được viết bằng C++, nên sẽ có chút khó khăn khi bạn muốn sử dụng các function của OpenCV trên C#.Net.

Tình huống mình gặp phải đó là trên app của mình có hiển thị ảnh ,với Winform app thì việc hiển thị ảnh hay dùng đối tượng Bitmap. Nhưng OpenCV xử lý ảnh dưới dạng ma trận là kiểu Cv::Mat. Mình mất thời gian để tìm hiểu convert giữa 2 kiểu dữ liệu này và cách làm như sau:

Để dùng OpenCV trên project.Net bạn cần phải xây dựng một class warpper, class này sẽ làm nhiệm vụ giao tiếp giữa C++ và C# như trong project của mình. Việc viết một class wrapper như thế nào mình sẽ viết chi tiết vào một topic khác ^^.
