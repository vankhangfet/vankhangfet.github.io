---
layout: post
title: Machine learning day 1
tags: [Machine learning]
---
 	
Series này mình sẽ viết về ML, các bài post sẽ được lược dịch từ [https://mlcourse.ai/](https://mlcourse.ai/). Cá nhân mình thấy thì đây là một trang học ML rất hay. Với mình, là một software engineer, mình cũng không thực sự tốt về toán, nên mình cần những ví dụ cụ thể, những đoạn code chạy được. Sau khi chạy xong, mình sẽ tìm hiểu tại sao code đó lại chạy và nguyên lý hoạt động ra sao. Step by step

Đối với các bài toán machine learning thì data rất quan trọng, nếu chúng ta cho dữ liệu rác vào, thì kết quả đầu ra cũng sẽ là rác
"garbed in, garbed out". Đo đó việc hiểu và xử lý dữ liệu là một bước rất quan trọng. 

Day 1, chúng ta sẽ làm quan với Pandas, học cách load data vào data frame với Pandas. 

Code thôi! 

~~~

# import các thư viện cần thiết
import numpy as np
import pandas as pd 

#load data từ csv file vào data frame

df = pd.read_csv(".../.../data/telecom_churn.csv)
~~~

Kết thúc câu lệnh trên chúng ta đã load được csv vào data frame. Chúng ta có một số lệnh thao tác với data frame như sau:

~~~~
# Show data
df.head()
# Chúng ta sẽ có kết quả như sau: 

0	KS	128	415	No	Yes	25	265.1	110	45.07	197.4	99	16.78	244.7	91	11.01	10.0	3	2.70	1	False
1	OH	107	415	No	Yes	26	161.6	123	27.47	195.5	103	16.62	254.4	103	11.45	13.7	3	3.70	1	False
2	NJ	137	415	No	No	0	243.4	114	41.38	121.2	110	10.30	162.6	104	7.32	12.2	5	3.29	0	False
3	OH	84	408	Yes	No	0	299.4	71	50.90	61.9	88	5.26	196.9	89	8.86	6.6	7	1.78	2	False
4	OK	75	415	Yes	No	0	166.7	113	28.34	148.3	122	12.61	186.9	121	8.41	10.1	3	2.73	3	False

# Liệt kê số lượng bản ghi và features

print(df.shapes)
(3333,20)

~~~~
