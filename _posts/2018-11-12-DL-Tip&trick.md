---
layout: post
title: Deep Learning Tips and Tricks
tags: [Machine learning]
---

Trong post này mình sẽ tìm hiểu một số Tips and Tricks để làm cho model deep learning đạt kết quả cao hơn.
Việc optimize một model deep learnign tốn khá nhiều thời gian và công sức vì chúng ta phải kiểm nghiệm model thì mới biết được model tốt hay không tốt, vì trong mạng deep learning có quá nhiều tham số, việc optimize đó đòi hỏi một cấu hình phần cứng rất mạnh mẽ. Nên rất ít các kỹ sư có thể làm điều này. Tốt nhất là chúng ta nên xây dựng mạng dựa trên những kiến trúc đã được chứng minh là chạy tốt và phù hợp với domain của mình. 

### Deep Learning Techniques
Có một số kỹ thuật sẽ giúp bạn cải thiện độ chính xác của deep learning model với Pre-trained model:

1. Tìm hiểu về ý tưởng của kiến trúc pre-trained mode:
Bạn sẽ biết được lợi thế của transfer learning và làm quen với một số kiến trúc CNN có hiệu năng tốt. Sau đó bạn nên đánh giá domain của bạn và bài toán, mặc dù domain áp dụng có thể khác nhau, nhưng những feature mà pre-trained model có thể giúp cho model của bạn hoạt động tốt.

2. Bắt đầu với learning rate nhỏ:
Vì sử dụng pre-trained model, nên trọng số của weight đã được xác định, nên chúng ta sẽ đánh giá model với learning rate nhỏ sau đó sẽ đáng giá độ hội tụ sau mỗi epochs.

3. Cải thiện model bằng kỹ thuật Drop:

Việc bạn cài đặt tham số Drop không có một quy tắc chung, điều này phụ thuộc vào bài toán của bạn, và quá trình test. 

4. Limit weight sizes:

Chuẩn hóa model bằng cách limit norm (absolute value)

5. Không thay đổi first layer:

6. Modify output layer: Tùy thuộc vào bài toán, bạn phải thay đổi output cho phù hợp.

OK!, như vậy chúng ta đã đi qua 6 kỹ thuật để cải thiện model. Bây giờ chúng ta sẽ xem việc thực hiện qua Keras như thế nào?

### Techniques in Keras

Ở ví dụ này, chúng ta sẽ thực hiện chỉnh sủa hệ số dropout và limit weight với Keras và bài toán MNIST

~~~~
# dropout in input and hidden layers
# weight constraint imposed on hidden layers
# ensures the max norm of the weights does not exceed 5
model = Sequential()
model.add(Dropout(0.2, input_shape=(784,))) # dropout on the inputs
# this helps mimic noise or missing data
model.add(Dense(128, input_dim=784, kernel_initializer='normal', activation='relu', kernel_constraint=maxnorm(5)))
model.add(Dropout(0.5))
model.add(Dense(128, kernel_initializer='normal', activation='tanh', kernel_constraint=maxnorm(5)))
model.add(Dropout(0.5))
model.add(Dense(1, kernel_initializer='normal', activation='sigmoid'))
~~~~




Bài viết được mình lược dịch từ link sau:

https://towardsdatascience.com/deep-learning-tips-and-tricks-1ef708ec5f53
