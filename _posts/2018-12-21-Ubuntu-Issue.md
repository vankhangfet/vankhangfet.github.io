---
layout: post
title: Một số issue của Ubuntu.
tags: [Ubuntu]
---

Dạo gần đây mình phải sử dụng Ubuntu để làm việc, việc chuyển từ Windows sang Ubuntu cũng có chút lạ lẫm. Với Ubuntu bạn phải làm quen với
việc dùng nhiều câu lệnh hơn. Trước khi setup môi trường ngon lành, mình gặp phải một số vấn đề sau:

## 1. Proxy setting cho terminal 
Các bạn thực hiện step dưới đây:

### 1.1 For apt,software center etc
Edit the file /etc/apt/apt.conf

And then replace all the existing text by the following lines
~~~~
Acquire::http::proxy "http://username:password@host:port/";
Acquire::ftp::proxy "ftp://username:password@host:port/";
Acquire::https::proxy "https://username:password@host:port/";
~~~~

### 1.2 Edit the file /etc/environment
And then add the following lines after PATH="something here"

~~~~
http_proxy=http://username:password@host:port/
ftp_proxy=ftp://username:password@host:port/
https_proxy=https://username:password@host:port/
~~~~
