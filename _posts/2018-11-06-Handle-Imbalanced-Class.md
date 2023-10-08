---
layout: post
title: Xử lý imbalanced classes trong machine learning
tags: [Machine learning]
---
Imbalanced classes có ảnh hưởng rất lớn tới độ chính xác của model. Nhưng hiện tượng mất cân bằng này lại là một hiện tượng rất hay xảy ra trong các bài toán machine learning. Khi xử lý dữ liệu imbalanced như vậy, chúng ta sẽ không thể xử lý dữ liệu theo cách thông thường được, cần một số kỹ thuật để giải quyết. Trước khi đi sâu vào kỹ thuật, thì Imbalanced classed hay xảy ra ở một số domain sau:
1. Fraud detection (Phát hiện bất thường)

2.Spam filtering (Filter thông tin Spam)

4.Disease screening (Sàng lọc dữ liệu bệnh )

5.SaaS subscription churn (Việc ngưng xử dụng dịch vụ)

6.Advertising click-throughs (Quảng cáo thông qua click)

Trong post này chúng ta sẽ tìm hiểu 5 kỹ thuật xử lý imbalance data.

Chúng ta hãy xem xét một tình huống như sau. Với dữ liệu bệnh, bạn cần xây dựng model để dự đoán bệnh nhân có khả năng có bệnh hay không có bệnh qua dữ liệu đầu vào là chỉ số sinh học, tuy nhiên khách hàng lại cho chúng ta dữ liệu mà chỉ có 8% bệnh nhân có dấu hiệu bệnh.

Nếu như code của bạn chỉ là 
~~~~
def disease_screen(patient_data):
    # Ignore patient_data
    return 'No Disease.'
~~~~

Thì model của bạn đã đạt đến độ chính xác 92%? Nhưng việc phát hiện bệnh sẽ quan trong hơn việc bỏ qua bệnh, do đó 92% trong trường hợp này sẽ không có ý nghĩa.

OK!, chúng ta cần một số kỹ thuật để xử lý imbalanced dataset. Không phải tất cả những kỹ thuật có hiệu quả, nhưng hầu hết các kỹ thuật dưới đây sẽ có tác dụng.

### Balance Scale Dataset
Ở đây chúng ta sẽ dùng một dữ liệu mẫu là Balance Scale Data, các bạn có thể download dữ liệu này từ UCI Machine learning. 
Link [http://archive.ics.uci.edu/ml/datasets/balance+scale](http://archive.ics.uci.edu/ml/datasets/balance+scale).

Chúng ta hãy xem view data:

~~~~
import pandas as pd
import numpy as np

# Read dataset
df = pd.read_csv('balance-scale.data', 
                 names=['balance', 'var1', 'var2', 'var3', 'var4'])
 
# Display example observations
df.head()
~~~~

### The Danger of Imbalanced Classes

~~~~
#Import algorithm and accuracy metricPython

from sklearn.linear_model import LogisticRegression

from sklearn.metrics import accuracy_score

#Next, we'll fit a very simple model using default settings for everything.

#Train model on imbalanced dataPython

#Separate input features (X) and target variable (y)

y = df.balance
X = df.drop('balance', axis=1)
 
#Train model
clf_0 = LogisticRegression().fit(X, y)
 
#Predict on training set
pred_y_0 = clf_0.predict(X)

#How's the accuracy?
print( accuracy_score(pred_y_0, y) )
# 0.9216
~~~~

Nêu như chúng ta training model train thì kết quả chính xác là 92%, tuy nhiên khi kiểm tra kết quả dự đoán thực tế thì 
#Should we be excited?
print( np.unique( pred_y_0 ) )

Kết quả dự đoán hoàn toàn sai. Chúng ta hãy thử áp dụng kỹ thuật đầu tiên

### 1. Up-sample Minority Class
Ý tưởng của kỹ thuật này là tăng số lượng class có số lượng ít nên, để làm cho dữ liệu cân bằng hơn.
Trong Scikit-Learn đã cung cấp sẵn cho ta module để thực hiện việc này:

~~~~
from sklearn.utils import resample
# Separate majority and minority classes
df_majority = df[df.balance==0]
df_minority = df[df.balance==1]
 
# Upsample minority class
df_minority_upsampled = resample(df_minority, 
                                 replace=True,     # sample with replacement
                                 n_samples=576,    # to match majority class
                                 random_state=123) # reproducible results
 
# Combine majority class with upsampled minority class
df_upsampled = pd.concat([df_majority, df_minority_upsampled])
 
# Display new class counts
df_upsampled.balance.value_counts()
# 1    576
# 0    576
# Name: balance, dtype: int64
~~~~
Khi dữ liệu đã balance chúng ta hãy kiểm thử model 
~~~
#Separate input features (X) and target variable (y)
y = df_upsampled.balance
X = df_upsampled.drop('balance', axis=1)
 
#Train model
clf_1 = LogisticRegression().fit(X, y)
 
#Predict on training set
pred_y_1 = clf_1.predict(X)
 
#Is our model still predicting just one class?
print( np.unique( pred_y_1 ) )
# [0 1]
 
# How's our accuracy?
print( accuracy_score(y, pred_y_1) )
# 0.513888888889
~~~~ 

Bây giờ độ chính xác chỉ đạt 51%.

Bài này mình lược dịch từ link sau: https://elitedatascience.com/imbalanced-classes
