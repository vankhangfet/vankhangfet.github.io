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

Source code thì bạn có thể tìm thấy tại đây 
[U-net source](https://github.com/brine-io/u-net-segmentation-example/blob/master/U-Net%20Furniture%20Segmentation%20Example.ipynb)

Bài toán của chúng ta sẽ là thực hiện segmentation chiếc ghế. Việc đầu tiên cần làm là download dataset:
~~~~
brine install rohan/chairs-with-masks
~~~~
Trong dataset gồm 97 images, khi training và test chúng ta sẽ chia làm 2 fold Validation: 20 Training: 77 

Ta thực hiện chia dữ liệu bằng Keras như sau:
~~~~
train_generator = train_fold.to_keras(
    'image',
    'mask',
    batch_size=BATCH_SIZE,
    shuffle=True, 
    processing_function=train_process)
validation_generator = validation_fold.to_keras(
    'image',
    'mask',
    batch_size=BATCH_SIZE,
    shuffle=False,
    processing_function=validation_process)
~~~~

Và dưới đây là một số kết quả:

![Result1](https://cdn-images-1.medium.com/max/800/1*nD5-fCILU7XGrXIDCSWr-A.png "Result1")



Bài này mình lược dịch từ link sau:
https://medium.com/@hanrelan/a-non-experts-guide-to-image-segmentation-using-deep-neural-nets-dda5022f6282
