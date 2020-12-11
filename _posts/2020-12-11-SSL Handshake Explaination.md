---
layout: post
title: Note về SSL và Handshake trong SSL.
tags: [Others]
---

Trước khi đi chi tiết vào quá trình "Handshake" thì như các bạn đã biết HTTPS là một giao thức rất phổ biến hiện nay. Vậy HTTPS là gì? 

HTTPS = HTTP + SSL 

Khi bạn open browser và gõ một url ví dụ "https://abc.xyz" thì sau đó browser và webserver tạo một kết nối https sử dụng one-way SSL Handshake. 
Mục đích của quá trình "Handshake" này là cung cấp quyền riêng (privacy) tư và tính toàn vẹn của dữ liệu (data integrity) để giao tiếp giữa server và client. Trong quá trình "Handshake", server và client sẽ trao đổi thông tin quan trọng cần thiết để thiết lập kết nối an toàn.

Có 2 kiểu trong quá trình bắt tay (SSL handshakes) đó là:
1. One-way SSL --> Trong quá trình one-way thì client sẽ validate tính xác thực của server. 
2. Two-way SSL (Mutual SSL) --> Quá trình này thì server và client sẽ xác thực danh tính lẫn nhau. 

Với https, thì one-way SSL được sử dụng, lúc này client sẽ validate danh tính (identity) của server. Two-way SSL được sử dụng trong quá trình giao tiếp 
server -> server khi cả 2 cần xác thực lẫn nhau.

