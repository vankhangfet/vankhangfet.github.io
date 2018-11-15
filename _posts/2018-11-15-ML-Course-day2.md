---
layout: post
title: Machine learning day 2 - Introduce Kaggle Kernels
tags: [Machine learning]
---
Khi học ML tốt nhất là nên thực hành, trong post này mình sẽ giới thiệu với các bạn một website để chia sẻ data, cũng như thử nghiệm các model. 

Nếu như làm về data và ML chắc hẳn các bạn đã biết trang web sau:[https://www.kaggle.com](https://www.kaggle.com).

Kaggle là một platform để thực hiện và chia sẻ dữ liệu giữa các bạn làm data. Trên site cũng có tổ chức các cuộc thi và phần thưởng cho các bạn tham gia. Đây là một site rất hay để học hỏi và thực hành data từ cộng đồng.

Khi tham gia và Kaggle các bạn sẽ gặp một cụm từ đó là Kaggle Kernels. Vậy Kaggle Kernels là gì? và chúng ta sẽ làm gì với Kagg Kernels?

### 1. Kaggle Kernels 

Kaggle Kernels là một free platform để chạy môi trường Jupyter notebooks trên trình duyệt. Điều này có nghĩa là bạn có thể save lại những cấu hình trong notebooks của bạn trên trình duyệt, miễn sao máy tính của bạn có kết nối internet. 

Ngoài ra những xử lý trên notebooks của bạn được thực hiện trên server, do đó sẽ không ảnh hưởng tới hiệu năng của máy tính. Nếu như bạn chạy trên laptop thì việc này không tiêu tốn battery của bạn.

### 2. Kaggle Kernels in Action. 

Vậy chúng ta đã biết Kaggle Kernels là gì? Hãy bắt đầu code thôi, vì mình là software engineer, nên phải code hello world đã. 
Đầu tiên chúng ta phải tạo một acc trên Kaggle. Sau đó create kernels đầu tiên.

![alt text](https://cdn-images-1.medium.com/max/1000/1*4CAxeDfReJem2kb4xdyxlQ.gif "Logo Title Text 1")

Kernels cung cấp cho các bạn tài nguyên để làm, nhưng cũng khá hạn chế. Cấu hình và tham số của kernels như hình dưới đây:

![resource](https://cdn-images-1.medium.com/max/600/1*m5HugLX1_rci6b7sjNzb-A.png "resource")

Các bạn có thể chạy một process tối đa là 60 phút.

OK, sau khi có data và môi trường, chúng ta đã có thể viết code được rồi. Hãy thử chạy một đoạn đơn giản như sau xem sao:

~~~~
import numpy as np # linear algebra
import pandas as pd # data processing, CSV file I/O (e.g. pd.read_csv)

# Input data files are available in the "../input/" directory.
# For example, running this (by clicking run or pressing Shift+Enter) will list the files in the input directory

import os
print(os.listdir("../input/")) 

import tensorflow as tf 
print(tf.__version__)

data_train_file = "../input/fashion-mnist_train.csv"
data_test_file = "../input/fashion-mnist_test.csv"

df_train = pd.read_csv(data_train_file)

df_test = pd.read_csv(data_test_file)

df_train.head()
~~~~

Chúng ta sẽ thấy kết quả như sau:

![result](https://cdn-images-1.medium.com/max/1000/1*YYQlICEzYk5p8T8RhoS4nw.png "result")

Vậy là chúng ta đã biết cách tạo một Kaggle kernerls và thực hành ML với các data từ cộng đồng rồi.

Bài viết mình có tham khảo link sau:

[https://towardsdatascience.com/introduction-to-kaggle-kernels-2ad754ebf77](https://towardsdatascience.com/introduction-to-kaggle-kernels-2ad754ebf77)
