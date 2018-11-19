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





Bài viết mình lược dịch từ [https://leonardoaraujosantos.gitbooks.io/artificial-inteligence/content/image_segmentation.html](https://leonardoaraujosantos.gitbooks.io/artificial-inteligence/content/image_segmentation.html)
