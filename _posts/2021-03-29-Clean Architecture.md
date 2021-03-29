---
layout: post
title: Xây dựng một kiến trúc theo style Clean Architecture như thế nào?
tags: [DESIGN]
---

Dạo gần đây thì mình có tìm hiểu về design, cũng như áp dụng Clean Architecture vào trong các dự án. Theo cá nhân mình thấy thì Clean Architecture khá dễ hiểu? 

Có rất nhiều tác giả viết về vấn đề này. Mình chỉ note lại một số điểm chính. Dù kiến trúc nào thì cũng nên tuẩn thủ các principles như sau: 

Architectural principles

- Separation of concerns

- Encapsulation

Các phần khác nhau của ứng dụng nên có tính đóng gói (Encapsulation) để hạn chế tối đa ảnh hưởng chúng với các phần khác của ứng dụng. Các thành phần này có thể trong nội bộ của chúng mà không phá vỡ, ảnh hướng tới các thành phần bên ngoài khác. Việc sử dụng tính năng đóng gói đúng cách sẽ giúp đạt được thiết kế mềm dẻo và tính mô-đun hóa, vì các đối tượng đóng gói có thể được thay thế bằng cách giữ nguyên interface.

- Dependency inversion

 The direction of dependency within the application should be in the direction of abstraction, not implementation details.
 Đơn giản dễ hiểu thì chúng ta nên thiết kế sao cho layer trên không phụ thuộc trực tiếp vào layer dưới, chúng nên giao tiếp thông qua interface. 
 Ví dụ dưới đây là một thiết kế tốt khi không sử dụng và có sử dụng DI
 
 ![No-DI](https://docs.microsoft.com/en-us/dotnet/architecture/modern-web-apps-azure/media/image4-1.png "No-DI")
 
 ![DI](https://docs.microsoft.com/en-us/dotnet/architecture/modern-web-apps-azure/media/image4-2.png "DI")
 
 
- Explicit dependencies

- Single responsibility

![architecture](https://docs.microsoft.com/en-us/dotnet/architecture/modern-web-apps-azure/media/image5-7.png "architecture")
