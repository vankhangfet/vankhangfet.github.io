---
layout: post
title: Image segmentation using Deep learning
tags: [Machine learning]
---
Trong Post trước chúng ta đã tìm hiểu cách thức convert mạng CCN thành FCN để thực hiện segmenation image. Hôm nay posy này mình sẽ tìm hiểu cụ thể segmentation image như thế nào trong deep learning với Python và Keras. Khi segmentation thì mục tiêu của chúng ta như sau:

Input image:

![Image_Segmen1](https://cdn-images-1.medium.com/max/800/1*qDTZb2PCoM-ZTzLZMqOrSQ.png "Image_Segmen1")

Output image:

![Image_Segmen2](https://cdn-images-1.medium.com/max/800/1*d8LA_ZJbeGfIAECjAGy5_A.png "Image_Segmen2")

Để thực hiện bài toán, chúng ta sẽ sử dụng Keras và U-net. U-net là một kiến trúc mạng cho bài toán image segmentation. Mạng này ban đầu được thiết kế cho bài toán trong biomedical, tuy nhiên nó cũng làm việc được trên những ảnh 2D thông thường. Các bạn sẽ thấy rằng mạng U-net này hoạt động tốt như thế nào với cả trường hợp dataset là không quá lớn.


Bài này mình lược dịch từ link sau:
https://medium.com/@hanrelan/a-non-experts-guide-to-image-segmentation-using-deep-neural-nets-dda5022f6282
