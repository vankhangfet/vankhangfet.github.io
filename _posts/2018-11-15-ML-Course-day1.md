---
layout: post
title: Machine learning day 1 - Làm quen với Pandas
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

Tiếp đến, chúng ta sẽ xem dữ liệu có những colum như thế nào?

~~~~
print(df.columns)

# Kết quả như sau:
Index(['State', 'Account length', 'Area code', 'International plan',
       'Voice mail plan', 'Number vmail messages', 'Total day minutes',
       'Total day calls', 'Total day charge', 'Total eve minutes',
       'Total eve calls', 'Total eve charge', 'Total night minutes',
       'Total night calls', 'Total night charge', 'Total intl minutes',
       'Total intl calls', 'Total intl charge', 'Customer service calls',
       'Churn'],
      dtype='object')
~~~~
Ngoài ra ta cũng có thể xem được thuộc tính của các features có kiểu dữ liệu là gì
~~~~
print(df.info())
~~~~

Trong Pandas cũng hỗ trỡ các thao tác như sorting, indexing và truy cập data. 
~~~~
# Sorting data
df.sort_values(by=['Churn','Total day charge'], ascending=[True,False]).head()
~~~~

~~~~
# Indexing data 
df['Churn'].mean()
~~~~

Chúng ta cũng có thể add thêm cột vào dataframe(DataFrame transformations). Cú pháp rất đơn giản:

~~~~
# Add new colum "total_calls"
total_calls = df['Total day calls'] + df['Total eve calls'] + \
              df['Total night calls'] + df['Total intl calls']
df.insert(loc=len(df.columns), column='Total calls', value=total_calls) 
# View data after new column is added
df.head()
~~~~
Tuy nhiên có một cách khác để add thêm cột đó là:
~~~~
df['Total charge'] = df['Total day charge'] + df['Total eve charge'] + \
                     df['Total night charge'] + df['Total intl charge']
df.head()
~~~~

Ngoài việc add thêm column thì Pandas cho phép chúng ta dễ dàng, xóa bỏ cột (drop)

~~~~
# get rid of just created columns
df.drop(['Total charge', 'Total calls'], axis=1, inplace=True) 
# and here’s how you can delete rows
df.drop([1, 2]).head()

State	Account length	Area code	International plan	Voice mail plan	Number vmail messages	Total day minutes	Total day calls	Total day charge	Total eve minutes	Total eve calls	Total eve charge	Total night minutes	Total night calls	Total night charge	Total intl minutes	Total intl calls	Total intl charge	Customer service calls	Churn
0	KS	128	415	False	True	25	265.1	110	45.07	197.4	99	16.78	244.7	91	11.01	10.0	3	2.70	1	0
3	OH	84	408	True	False	0	299.4	71	50.90	61.9	88	5.26	196.9	89	8.86	6.6	7	1.78	2	0
4	OK	75	415	True	False	0	166.7	113	28.34	148.3	122	12.61	186.9	121	8.41	10.1	3	2.73	3	0
5	AL	118	510	True	False	0	223.4	98	37.98	220.6	101	18.75	203.9	118	9.18	6.3	6	1.70	0	0
6	MA	121	510	False	True	24	218.2	88	37.09	348.5	108	29.62	212.6	118	9.57	7.5	7	2.03	3	0

~~~~



Các bạn chú ý, khi set "inplace = True" chúng ta sẽ trực tiếp tác động đến Data frame. Tham số axis =0 nghĩa là drop row, 1 drop column.




Như vậy là các bạn đã làm quen với một số lệnh cơ bản, chi tiết hơn các bạn tham khảo link sau:
[https://mlcourse.ai](https://mlcourse.ai/notebooks/blob/master/jupyter_english/topic01_pandas_data_analysis/topic1_pandas_data_analysis.ipynb?flush_cache=true)

