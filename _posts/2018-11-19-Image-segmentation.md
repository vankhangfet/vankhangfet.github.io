---
layout: post
title: Image Segmentation trong convolutional neural networks (CNN)
tags: [Machine learning]
---
### Introduction

Như các bạn đã biết thì very deep CNN có thể phân loại các object rất tốt, ngoài ra thì CNN cũng có ứng dụng vào image segmenation nữa. Post này chúng ta sẽ tìm hiểu xem. Mạng CNN sẽ segmen image như thế nào? Mình viết bài này vì rất tò mò muốn biết ý tưởng segmen image sử dụng CNN ra sao?

Hãy xem ví dụ một bức ảnh dưới đây và mục tiêu chúng ta muốn segmentation.

![Image_Segmen](https://leonardoaraujosantos.gitbooks.io/artificial-inteligence/content/image_folder_3/ImageSegmentation.PNG "Image_Segmen")

### Fully Convolutional network for segmentation

Một mạng fully convolutional neural network (FCN) là một mạng CNN, với layer fully connected cuối được thay thế bởi lớp tích chập khác với một large "receptive field". Ý tưởng là chụp lại nội dung tổng thể của bức hình.

![Image_Segmen1](https://leonardoaraujosantos.gitbooks.io/artificial-inteligence/content/image_folder_3/Fully_Convolutional_Network_Semantic.PNG "Image_Segmen1")

Ý tưởng ở đây là khi chuyển từ mạng CNN sang FCN, chúng ta chọn layer cuối cùng đủ lớn khi đó chúng ta sẽ có thể scaled up nên kích thước của input image.

![Image_Segmen2](https://leonardoaraujosantos.gitbooks.io/artificial-inteligence/content/image_folder_7/FCN.jpg "Image_Segmen2")

### Conversion from normal CNN to FCN
Ý tưởng là vậy, giờ chúng ta hãy xem cách convert một mạng CNN sang FCN. Ở ví dụ này chúng ta sẽ convert mạng Alexnet to FCN để sử dụng cho việc segmentation. Chúng ta hãy xem lại kiến trúc của mạng Alexnet 

![Image_Segmen2](https://leonardoaraujosantos.gitbooks.io/artificial-inteligence/content/image_folder_7/AlexNet_2.png "Image_Segmen2")

Hình dưới đây là số lượng tham số trong mạng Alexnet

![Image_Segmen3](https://leonardoaraujosantos.gitbooks.io/artificial-inteligence/content/image_folder_7/AlexNet_1.jpg "Image_Segmen3")

Trong mạng Alexnet, kích thước ảnh được cố định 224x224, vậy nên tác động của pooling sẽ làm giảm kích thước ảnh từ 224x224 thành các kích thước 55x55, 27x27, 13x13, sau đó đến cuối cùng là một vector ở FC layer

![Image_Segmen4](https://leonardoaraujosantos.gitbooks.io/artificial-inteligence/content/image_folder_7/AlexNet_0.jpg "Image_Segmen4")




Bài viết mình lược dịch từ [https://leonardoaraujosantos.gitbooks.io/artificial-inteligence/content/image_segmentation.html](https://leonardoaraujosantos.gitbooks.io/artificial-inteligence/content/image_segmentation.html)
