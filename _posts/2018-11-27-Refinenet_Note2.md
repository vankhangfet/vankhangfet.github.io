---
layout: post
title: How to run Refinenet with Matlab
tags: [Machine learning]
---

Trong post trước[https://vankhangfet.github.io/2018-11-16-Quicknote-refinenet/](https://vankhangfet.github.io/2018-11-16-Quicknote-refinenet), chúng ta đã tìm hiểu cơ bản về Refinenet. Bài này chúng ta sẽ chạy thử source code với RefineNet trên Matlab xem kết quả như thế nào? 

Để chạy được source code trên Matlab, chúng ta cần chuẩn bị môi trường sau:
1. VS C++ 2015 
2. MatLab 2018 
3. Source code refine net:
   [https://github.com/guosheng/refinenet](https://github.com/guosheng/refinenet)
   
Nếu như các bạn muốn tự mình training mạng này thì phải download thêm dataset từ 
[http://host.robots.ox.ac.uk/pascal/VOC/voc2012/](http://host.robots.ox.ac.uk/pascal/VOC/voc2012/), việc training khác tốn thời gian, nên mình sẽ dùng thử pre-trained model và xem kết quả của mạng RefineNet như thế nào? 

Về pre-trained model các bạn có thể download tại đây:
[https://libraries.io/github/ZhaoJ9014/refinene](https://libraries.io/github/ZhaoJ9014/refinene)

OK! khi đã chuẩn bị môi trường và source code xong, chúng ta làm các bước sau:

1. Build thư viện matconvnet. Các bạn tham khảo tại link sau [http://www.vlfeat.org/matconvnet/install/(http://www.vlfeat.org/matconvnet/install/).

Chúng ta load source code vào môi trườn Matlab. Sau đó thực hiện command sau:
 - cd 

 

2. Sau khi đã build xong
