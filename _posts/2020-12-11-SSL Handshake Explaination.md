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
server -> server khi cả 2 cần xác thực lẫn nhau. Quá trình bắt tay gồm các steps như sau: 

![handshake-process](/img/ssl-tls-handshake-process.png "handshake-process")

1. Client Hello

Client send thông tin được yêu cầu bởi server để thiết lập HTTPS connection. 

~~~~
*** ClientHello, TLSv1.2
RandomCookie: *** ClientHello, TLSv1.2
RandomCookie: GMT: -1892413556 bytes = { GMT: -351008774 bytes = { 169, 131, 204, 213, 154, 96, 7, 136, 43, 142, 232, 138, 148, 171, 52, 226, 155, 202, 145, 57, 210, 132, 227, 182, 67, 222, 161, 28, 20 }
Session ID: 239, 10, 92, 143, 185, {}
93, Cipher Suites: [Unknown 0x8a:0x8a, TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256, TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256, TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384, TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384, Unknown 0xcc:0xa9, Unknown 0xcc:0xa8, TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA, TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA, TLS_RSA_WITH_AES_128_GCM_SHA256, TLS_RSA_WITH_AES_256_GCM_SHA384, TLS_RSA_WITH_AES_128_CBC_SHA, TLS_RSA_WITH_AES_256_CBC_SHA, SSL_RSA_WITH_3DES_EDE_CBC_SHA]
………………………………………………
~~~~

Chúng ta có thể thấy client hello với TLS v1.2. Danh sách "Cipher" được support bởi client cũng được gửi kèm. Nếu như server không hỗ trợ những "Cipher"
này thì server sẽ ignore. Trong trường hợp này server gửi failuer alert và đóng kết nối (close connection)



