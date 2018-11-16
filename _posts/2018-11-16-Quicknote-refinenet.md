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




