---
layout: post
title: Một số khái niệm cơ bản.
tags: [Others]
---

Kiến thức nền tảng hay những khái niệm cơ bản đóng vai trò rất quan trọng. Mình có nhận thấy rằng mặc dù đã có kinh nghiệm làm việc, tuy nhiên một số bạn Dev vẫn cảm thấy lúng túng khi giải thích một số vấn đề. Bài này mình sẽ điểm qua những thứ cơ bản đó

# 1. Sự khác nhau giữa process và thread là gì?

Process có thế được coi là tiến trình, hay một application. Ví dụ khi ta click một icon MSWord trên màn hình desktop ta đang khởi tạo một tiến trình Word. Khi tiến trình này khởi động thì có thể có rất nhiều thread trong tiến trình này được chạy, ví dụ như thread chuẩn bị data,vv... Khi bạn khởi động chương trình Word, hệ thống sẽ tạo ra một process bắt đầu với thread main của process đó. 

Có một điểm quan trọng đó là thread có thể thực thi được các tác vụ mà process có thể làm. Process có thể gồm nhiều thread, nên có thể coi
thread là một phần rút gọn của process.

