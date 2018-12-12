---
layout: post
title: Why machine learning move to the Edge ?
tags: [Machine learning]
---

Trong post này mình sẽ tìm hiểu một xu hướng trong lĩnh vực machine learning và deep learning. Tại sao xu hướng move ML/DL tới Edge, Edge ở đây là đề cập tới các thiết bị cuối (End- device). Như chúng ta đã biết trong một số hệ thống nhận dạng, thì dữ liệu được thu nhận tại client nhưng dữ liệu được chuyển tới phía server để xử lý, sau đó server trả kết quả lại về client. Mô hình này là một giải pháp đầu tiên chúng ta nghĩ tới khi triển khai các hệ thống ML/DL. Tuy nhiên khi dữ liệu lớn và độ trễ của hệ thống cao hay như bảo mật lại một vấn đề cần quan tâm thì mô hình client- server lại nảy sinh nhiều issue. Do đó việc move ML/DL to Edge lại là một giải pháp tốt.

Khi move to Edge ta sẽ giải quyết được một số vấn đề như sau: 

1. Tối ưu bandwidth hơn.

2. Giảm Latancy 

3. Hệ thống sẽ security hơn.

4. Với những thiết bị embeded, mobile có thể tối ưu năng lượng hơn.

5. Giảm cost hơn.

Vậy thì move to Edge như thế nào? Do mình có thời gian tìm hiểu về việc deploy trên Arm nên mình sẽ bài này sẽ đề cập tới Arm.



https://petewarden.com/2016/05/03/how-to-quantize-neural-networks-with-tensorflow/comment-page-1/

https://developer.arm.com/technologies/machine-learning-on-arm/developer-material/how-to-guides/deploying-a-caffe-model-on-openmv-using-cmsis-nn/quantize-the-model
