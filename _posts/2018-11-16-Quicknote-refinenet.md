---
layout: post
title: Quick note - RefineNet
tags: [Machine learning]
---

Vì bản tính tò mò, nên mình rất thích tìm hiểu về Deep learning. Một phần vì do công việc, một phần mình cũng muốn ứng dụng DL vào bài toán của mình. Với một số bài toán, thì phương pháp xử lý ảnh thông thường cho kết quả không cao. Hơn nữa, chúng ta đang sống trong thời đại của BigData, Deep learning nên việc không biết những công nghệ này thì thật là đáng tiếc :)). Deep learning tỏ ra rất hiệu quả trong việc nhận diện object và segmentation. Tuy nhiên với những kiến trúc CNN, thì sẽ phát sinh những hạn chế như việc khi image đi qua nhiều lần pooling và tích chập kích thước của image sẽ giảm đi, do đó mà lượng thông tin sẽ mất đi. Kết quả là việc segmentation sẽ không còn chính xác nữa. Để khắc phục hạn chế đó thì một nhóm tác giả đưa ra kiến trúc RefineNet để khắc phục nhược điểm này. 

Ý tưởng của RefineNet là tìm ra những thông tin trong quá trình down-sampling để tăng khả năng segmentation. Để biết thêm chi tiết, các bạn hãy đọc bài báo sau:

RefineNet: Multi-Path Refinement Networks for High-Resolution Semantic Segmentation.

Thực sự để hiểu một bài báo một cách chi tiết với mình thấy khá khó, nên mình note lại một số ý chính sau:

1. RefineNet khắc phục nhược điểm của mạng CNN, bằng cách lọc ra tất cả thông tin của bức ảnh trong quá trình down-sampling.
2. RefineNet được thiết kế để tối ưu cho memory và chi phí tính toán. 

Để hiểu hơn về RefineNet chúng ta hãy xem hình sau:

![refine_Net](/img/RefineNet.JPG "refine_Net")

Hình (a) là mạng CNN điển hình, giống như ResNet (a), thông tin bị mất đi sau mỗi lần tích chập. Để khắc phục điều này thể sử dụng Dilated Convolutions, tuy nhiên càng về sau thì số lượng ảnh lại càng nhiều nên. Điều này gây ra chi phí lớn về tính toán, dễ dàng gây ra thiếu hụt bộ nhớ, cho dù chúng ta sử dụng modern GPUs. Kiến trúc RefineNet là một kiến trúc giải quyết vấn đề này (c), thông tin sẽ được tìm ra tại mỗi stage của convolution và sau đó được tổng hợp lại để dự đoán trên ảnh high-resolution, mà không cần phải maintain một lượng rất lớn các feature map. Chi tiết hơn ta hay xem cấu trúc của một block RefineNet

![refine_Net_Block](/img/RefineNetBlock.JPG "refine_Net_Block")

Tạm thời mình dừng ở đây, mình sẽ quay lại khi có điều kiện tìm hiểu kỹ hơn về RefineNet.

