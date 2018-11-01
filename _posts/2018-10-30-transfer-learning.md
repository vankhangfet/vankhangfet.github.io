---
layout: post
title: Transfer learning
image: /img/CNN_Net.jpg
tags: [Machine learning]
---

Bài này sẽ giúp các bạn tìm hiểu kỹ thuật Transfer learning là gì? Chúng ta sẽ trả lời 2 câu hỏi

1. Transfer learning là gì?
2. Tại sao transfer learning lại có thể làm việc tốt?

Tất nhiên để hiểu rõ hơn Transfer learning làm việc như thế nào, ta hãy bắt tay thực hiện code một program ở cuối bài.
### Transfer learning là gì?
Nếu như bạn đặt câu hỏi này, nghĩa là bạn đang đến với Deep learning. Khi nhắc tới deep learning thì một khái niệm 
được nhắc đến rất nhiều, mà các bạn hay gặp đó là CNN (Convolution Neural Networks). 

Mạng CNN có thể học và mapping được những function rất phực tạp khi có đủ data. Chúng ta vẫn không thể hoàn toàn hiểu
convnet học như thế nào. Về cơ bản thì một mạng CNN sẽ có cấu trúc như sau:

![Cnn Net](/img/CNN_Net.jpg "Cnn Net")

Và quá trình training mạng CNN là tìm ra giá trị thích hợp cho mỗi filter để trích xuất thông tin ảnh đầu vào, khi bức ảnh được
đi qua nhiều Convnet layer. 
Thông trích xuất này sẽ được làm đầu vào cho mạng neuron cho việc output kết quả đầu ra.

Việc training một mạng CNN từ đầu chỉ phù hợp với những project cỡ nhỏ, hầu hết các ứng dụng deep learning yêu cầu một dữ liệu
rất lớn, cũng như rất nhiều CNN layer. Việc này tiêu tốn rất nhiều tài nguyên và công sức. 

Đó là lý do tại sao chúng ta cần đến Transfer learning. Khi sử dụng Transfer learning, chúng ta sử dụng lại pre-trained weights
từ model đã được train trước đó (model này đã được train với hàng triệu image với rất nhiều category khác nhau, với GPU cấu hình 
cao.) và sử dụng lại những feature đã được học để dự đoán một class mới.

Như vậy transfer learning có những ưu điểm sau:
1. Không cần một training dataset lớn.
2. Không yêu cầu hệ thống có sức mạnh tính toán lớn. Khi sử dụng transfer learning chúng ta chỉ phải training một vài layer cuối.

Hiện nay có một số pre-train model đã được train trên tập image net dataset rất lớn, và được open source là 
VGG-16, VGG-19, Inception-V3 etc. Các bạn có thể tham khảo tại trang web Keras.
