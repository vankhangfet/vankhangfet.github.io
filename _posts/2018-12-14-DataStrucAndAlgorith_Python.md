---
layout: post
title: Data structures and Agorithm in Python (1)
tags: [Python]
---

Cấu trúc dữ liệu và giải thuật là một chủ đề rất thú vị, đúng ra sẽ không nên gắn liền với một ngôn ngữ cụ thể nào. Tuy nhiên mình đang làm việc với Python nên cấu trúc dữ liệu và thuật toán sẽ được cài đặt trên Python. Thuật toán đầu tiên được đề cập đó là Recursion.

Đệ quy được dùng cũng khá phổ biển và nhiều khi đệ quy lại là một cách ngắn gọn để tiếp cận vấn đề. Thuật toán đệ quy có thể làm gì, hãy xem ứng dụng đơn giản dưới đây:

1. Factorial function: tính giai thừa (commonly denotes as n!)

2. Binary search

3. File system: trong folder chúng ta có thể thấy có rất nhiều folder, trong mỗi folder con lại có rất nhiều folder nữa. Việc quản lý và 
truy cập folder này cần dùng đến đệ quy.

OK! hãy thử giải quyết bài toán bằng Python xem sao.

- Factorial function:

~~~~
def factorial(n):
    if n==0:
       return 1
    else:
       return n* factorial(n-1)
~~~~
