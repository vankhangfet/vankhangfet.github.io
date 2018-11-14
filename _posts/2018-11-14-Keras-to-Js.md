---
layout: post
title: Convert Keras to Tensor flow JS
tags: [Machine learning]
---

Trong post này mình sẽ giới thiệu cho các bạn cách convert model keras để sử dụng cho các ứng dụng web. Với ứng dụng web hiện nay thì JS là
một thành phần không thể thiếu. Sẽ rất thú vị nếu site của bạn có một ứng dụng deep learning. 

OK! bạn đã sử dụng Keras thì sẽ không xa lạ gì với đoạn lệnh sau:

~~~~
with open("model_mobilenet.json", "w") as json_file:
    json_file.write(model.to_json())
~~~~

Đoạn code trên sẽ save model dưới định dạng json. Đây là định dạng rất phổ biến với các web API và JS.

Tiếp theo đó chúng ta sẽ convert model này để tensor flow JS có thể sử dụng được.

Step 1: Load model 

~~~~
from keras.models import model_from_json
from keras.utils.generic_utils import CustomObjectScope
with CustomObjectScope({'relu6': keras.applications.mobilenet.relu6,'DepthwiseConv2D': keras.applications.mobilenet.DepthwiseConv2D}):
    model = model_from_json(open('model_mobilenet.json').read())
~~~~

Step 2: Convert to JS 

import tensorflowjs as tfjs

tfjs.converters.save_keras_model(model, 'model_JS')

