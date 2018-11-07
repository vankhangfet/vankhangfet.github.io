---
layout: post
title: Xử lý imbalanced classes trong machine learning
tags: [Machine learning]
---
Imbalanced classes có ảnh hưởng rất lớn tới độ chính xác của model. Nhưng việc imbalanced classes này lại là một hiện tượng rất hay xảy ra trong các bài toán machine learning. Khi xử lý dữ liệu imbalanced như vậy, chúng ta sẽ không thể xử lý dữ liệu theo cách thông thường được, cần một số kỹ thuật để giải quyết. Trước khi đi sâu vào kỹ thuật, thì Imbalanced classed hay xảy ra ở một số domain sau:

1. Fraud detection (Phát hiện bất thường)
2.Spam filtering (Filter thông tin Spam)
4.Disease screening (Sàng lọc dữ liệu bệnh )
5.SaaS subscription churn (Việc ngưng xử dụng dịch vụ)
6.Advertising click-throughs (Quảng cáo thông qua click)

Trong post này chúng ta sẽ tìm hiểu 5 kỹ thuật xử lý imbalance data.


Bài này mình lược dịch từ link sau: https://elitedatascience.com/imbalanced-classes
