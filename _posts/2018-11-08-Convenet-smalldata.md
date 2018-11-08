---
layout: post
title: Deep learning với small data
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

Nếu bạn dùng command:

model.sumary()

Chúng ta sẽ có thông tin như sau:

Layer (type) Output Shape Param

conv2d_1 (Conv2D) (None, 148, 148, 32) 896

max_pooling2d_1 (MaxPooling2 (None, 74, 74, 32) 0

conv2d_2 (Conv2D) (None, 72, 72, 64) 18496

max_pooling2d_2 (MaxPooling2 (None, 36, 36, 64) 0

conv2d_3 (Conv2D) (None, 34, 34, 128) 73856

max_pooling2d_3 (MaxPooling2 (None, 17, 17, 128) 0

conv2d_4 (Conv2D) (None, 15, 15, 128) 147584

max_pooling2d_4 (MaxPooling2 (None, 7, 7, 128) 0

flatten_1 (Flatten) (None, 6272) 0

dense_1 (Dense) (None, 512) 3211776

dense_2 (Dense) (None, 1) 513

Total params: 3,453,121
Trainable params: 3,453,121
Non-trainable params: 0

### Data preprocessing
Để làm việc được mạng CNN thì dữ liệu đầu vào phải là matrix và giá trị của các phần tử trong matrix trong khoảng từ [0,1].
Chúng ta sẽ tiền xử lý dữ liệu trước khi đưa vào train cho mạng CNN.

~~~~
from keras.preprocessing.image import ImageDataGenerator

#All images will be rescaled by 1./255
train_datagen = ImageDataGenerator(rescale=1./255)
test_datagen = ImageDataGenerator(rescale=1./255)

train_generator = train_datagen.flow_from_directory(
        # This is the target directory
        train_dir,
        #All images will be resized to 150x150
        target_size=(150, 150),
        batch_size=20,
        #Since we use binary_crossentropy loss, we need binary labels
        class_mode='binary')

validation_generator = test_datagen.flow_from_directory(
        validation_dir,
        target_size=(150, 150),
        batch_size=20,
        class_mode='binary')
~~~~

OK! dữ liệu đã được xử lý ta có thể train model và lưu lại model như sau:

~~~~
history = model.fit_generator(
      train_generator,
      steps_per_epoch=100,
      epochs=30,
      validation_data=validation_generator,
      validation_steps=50)
            
model.save('cats_and_dogs.h5')
~~~~

Sau khi train xong, kiểm tra kết quả xem sao bằng command sau:

~~~~
import matplotlib.pyplot as plt

acc = history.history['acc']
val_acc = history.history['val_acc']
loss = history.history['loss']
val_loss = history.history['val_loss']

epochs = range(len(acc))

plt.plot(epochs, acc, 'bo', label='Training acc')
plt.plot(epochs, val_acc, 'b', label='Validation acc')
plt.title('Training and validation accuracy')
plt.legend()

plt.figure()

plt.plot(epochs, loss, 'bo', label='Training loss')
plt.plot(epochs, val_loss, 'b', label='Validation loss')
plt.title('Training and validation loss')
plt.legend()

plt.show()
~~~~

Kết quả của đoạn code trên cho ta đồ thì dưới đây. Dựa vào đồ thì ta có thể biết model hoạt động tốt hay không tốt? Có bị overfitting hay không?

Nhìn vào biểu đồ trên ta thấy rằng accuracy tăng theo thời gian và tiệm cận 100%, tuy nhiên validation accuracy chỉ dừng lại ở 70%.

Như vậy model có vẻ như bị overffiting. Để tránh hiện tượng overfitting ta sẽ thử tăng cường data xem sao.

### Using data augmentation
Trong Keras có hỗ trợ function để generate ra các ảnh khác nhau:
~~~~
atagen = ImageDataGenerator(
      rotation_range=40,
      width_shift_range=0.2,
      height_shift_range=0.2,
      shear_range=0.2,
      zoom_range=0.2,
      horizontal_flip=True,
      fill_mode='nearest')
~~~~

Nếu như traing mạng bằng các ảnh được generate thì ta có thể chắc chắn rằng mạng sẽ không bao giờ học 2 anh giống nhau. Tuy nhiên vì dữ liệu được generate ra từ một ảnh
gốc do đó ảnh sẽ không tự nhiên và vẫn sẽ có một tương quan nhất lớn nào đó, và dữ liệu đó không phải là dữ liệu mới. Do đó việc này cũng chưa thể tránh được hiện tượng overfitting.

Nên để tăng độ chính xác chúng ta cần thêm kỹ thuật Drop-out.
