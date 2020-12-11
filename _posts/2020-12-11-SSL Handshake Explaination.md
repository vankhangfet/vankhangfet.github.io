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

2. Server Hello
Server sẽ response client với configuration được select từ "Client hello" để thực hiện quá trình bắt tay 
~~~~
*** ServerHello, TLSv1.2
RandomCookie: GMT: 1518335451 bytes = { 19, 150, 56, 42, 168, 202, 151, 43, 174, 226, 187, 53, 135, 67, 244, 170, 59, 176, 105, 150, 50, 112, 167, 83, 192, 48, 171, 64 }
Session ID: {91, 128, 246, 219, 26, 93, 46, 172, 85, 212, 221, 79, 20, 186, 108, 134, 200, 239, 150, 102, 172, 24, 125, 171, 137, 53, 5, 130, 53, 228, 2, 195}
Cipher Suite: TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA
Compression Method: 0
Extension renegotiation_info, renegotiated_connection: <empty>
***
Server sẽ lựa chọn TLS version lower mà được suggest bởi client trong "Client Hello". Server cũng gửi lại thông tin "Cipher" được selecte từ danh sách "Cipher" mà client gửi lên.

Trong quá trình "Server Hello", server cũng gửi certificate của server cùng với "certificate chain". "Certificate chain" sẽ được validate trong client trust store. 

Để dễ hiểu ta có thể hình dung browser sẽ validate được "certificate chain" này.
~~~~
** Certificate chain
chain [0] = [
[
 Version: V3
 Subject: CN=server, OU=ID, O=IBM, L=Hursley, ST=Hants, C=GB
 Signature Algorithm: SHA256withRSA, OID = 1.2.840.113549.1.1.11

Key: Sun RSA public key, 2048 bits
 modulus: 17397562757879783124811507432494159361243533796048391161052829821122241422546147907779583980536886743765496985274573369668302996974964349098220930856827026983442125212118340479175872257401994146576001849503528844021528618702289642320157895787705650513758990004411195572445830613057931701313142946380207623174021376881040589912594451781207558263630010509870784494298596448861811827669869221033031956053367890915692918086795954628465637743034777850129818069833958463245749899713073673871721233098662285260745282530972322499603703844901496085490388703767606182211892402117158287170480970610942364235511256363933850852797
 public exponent: 65537
 Validity: [From: Sat Jul 28 09:08:48 IST 2018,
 To: Sun Jul 28 09:08:48 IST 2019]
 Issuer: CN=server, OU=ID, O=IBM, L=Hursley, ST=Hants, C=GB
 SerialNumber: [ 7d834874]
Certificate Extensions: 1
[1]: ObjectId: 2.5.29.14 Criticality=false
SubjectKeyIdentifier [
KeyIdentifier [
0000: C7 24 EA C3 1E 3E 58 8E BD E3 AE A9 17 01 00 51 .$…>X……..Q
0010: B0 83 D4 68 …h
]
]
]
 Algorithm: [SHA256withRSA]
 Signature:
0000: 4B FA 93 D8 56 78 05 D8 89 BC 2A 3A B6 C3 7F A5 K…Vx….*:….
0010: 03 D8 56 3B E6 9F 0B 17 B5 A2 61 AE 43 46 A4 85 ..V;……a.CF..
0020: 3F 60 2E 04 41 0D C2 7A 35 0D 56 F5 FE 9D 05 51 ?`..A..z5.V….Q
0030: 4A 0B BB 5B 30 ED 85 AF 1C 95 13 15 7D A0 2C DE J..[0………,.
0040: B4 A1 7A D0 5D E4 C0 91 37 C2 ED 37 39 65 7D 02 ..z.]…7..79e..
0050: B5 A4 72 FF EB 6C D5 F4 FD BC 32 FD 9F C8 3A 49 ..r..l….2…:I
0060: 53 64 F8 C6 A0 D6 DB 89 2C 36 60 97 8B 33 8F 95 Sd……,6`..3..
0070: 18 9C 1A F2 F8 F1 66 5E F3 0B 76 54 08 AB A9 88 ……f^..vT….
0080: 5D E9 2D 6B AE 6D 98 09 57 A0 2A 9E C6 6B 89 53 ].-k.m..W.*..k.S
0090: 8E B3 58 C3 8D 73 C5 D3 58 2F 68 F0 4E 0A EF 29 ..X..s..X/h.N..)
00A0: 54 95 00 34 6A C4 D2 56 22 64 05 F9 9F A4 81 44 T..4j..V"d…..D
00B0: 44 77 95 A7 86 5A D3 EE EA 8E 06 19 ED 94 F1 83 Dw…Z……….
00C0: F4 A1 F4 A0 76 94 02 40 30 C0 95 6A F2 4F 32 BB ….v..@0..j.O2.
00D0: 79 A2 1B 40 F5 EB 37 5B B7 0C FA 18 DE 04 18 7D y..@..7[……..
00E0: 5A 1A 95 D7 E7 00 4C 7F 3C 71 CE 8E 03 07 BD 50 Z…..L.<q…..P
00F0: 6D 49 52 75 66 D2 CA 45 AB B8 EE B1 C2 C9 72 8A mIRuf..E……r.
]
***
~~~~


~~~~
