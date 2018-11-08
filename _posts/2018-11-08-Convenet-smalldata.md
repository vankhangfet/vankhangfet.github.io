
---
layout: post
title: Hello world
tags: [Machine learning]
---
Deep learning với small data. 

Trong bài này chúng ta sẽ xây dựng một mạng convnets với dataset mà dữ liệu là không nhiều. Nhiệm vụ bài toán là
phân biệt Dog và Cat.

### Training a convnets from scratch on a small datasets
Trong thực tế khi xây dựng một ứng dụng deep learning, thì việc chúng ta collect được dataset đủ lớn khá là khó. Dataset có vài trăm ảnh tới hàng nghìn ảnh cũng
đã được coi là tạm dùng được khi bạn có ý định xây dựng một ứng dụng sử dụng Deep learning.
Để xây dựng mô hình dự đoán tốt và tránh được hiện tượng overfitting ta có những kỹ thuật sau: Regularization, Drop-out, Agumentation. Ví dụ phân biệt
Dog và Cat chúng ta sẽ sử dụng Agumentation và Drop-out để tăng độ chính xác từ 72% lên tới 82%.

### The relevance of deep learning for small-data problem
Như các bạn đã biết thì deep learning chỉ làm việc tốt khi ta có một tập dữ liệu rất lớn và một đặc tính nữa của deep learning đó là
khả năng extract feature tự động. Tuy nhiên với dữ liệu được chuẩn hóa và nhiệm vụ đơn giản thì vài trăm sample cũng khả năng để huấn luyện mô hình tốt.

### Building our network
Với những ảnh có kích thước lớn, chúng ta cần mạng phức tạp hơn, trong bài toán phân loại này ở đầu ra chúng ta có thể dùng sigmoid function cho single unit cuối.

Ngoài ra trong mạng CNN thì độ phức tạp của feature map thông thường từ 32 -> 128, trong khi đó feature map thì giảm dần từ 148x148 -> 7x7.

Implement mạng như sau:

~~~~
from keras import layers
from keras import models

model = models.Sequential()
model.add(layers.Conv2D(32, (3, 3), activation='relu',
                        input_shape=(150, 150, 3)))
model.add(layers.MaxPooling2D((2, 2)))
model.add(layers.Conv2D(64, (3, 3), activation='relu'))
model.add(layers.MaxPooling2D((2, 2)))
model.add(layers.Conv2D(128, (3, 3), activation='relu'))
model.add(layers.MaxPooling2D((2, 2)))
model.add(layers.Conv2D(128, (3, 3), activation='relu'))
model.add(layers.MaxPooling2D((2, 2)))
model.add(layers.Flatten())
model.add(layers.Dense(512, activation='relu'))
model.add(layers.Dense(1, activation='sigmoid'))

from keras import optimizers

model.compile(loss='binary_crossentropy',
              optimizer=optimizers.RMSprop(lr=1e-4),
              metrics=['acc'])
~~~~ 
