---
layout: post
title: Understanding Feedforward Neural Networks
image: /img/neuralnetworks.jpg
tags: [Machine learning]
---

Lý do mình viết về Neural Networks là trong quá trình làm việc, mình phải làm với một số bài toán có sử dụng machine leaning và tất nhiên giờ đang là thời đại của BigData và Deep learning nên mình cũng rất tò mò về những khái niệm này. Sau một thời gian tìm hiểu thì mình thấy thích làm về ML, vừa đọc vừa thử nghiệm, nên cách tốt nhất là note lại và cố gắng giải thích theo cách hiểu của mình. 

Trong machine learning thì Neural Networks là một phần cũng rất quan trọng, chúng ta hãy thử tìm hiểu về NN mà không cần quá nhiều kiến thức toán học xem sao.

### Feedforware Neural Network là gì?
![Neural_net](/img/neuralnetworks.jpg "Neural_net")
Post này chúng ta sẽ nghiên cứu về Feedforward Neural Networks hay tên gọi khác là Multi-layer Perceptrons.
Kiến trúc mạng Neural rất quan trọng và được sử dụng trong các mạng CNN or RNN. Để hiểu về mạng Neural Networks hoạt
động ra sao, các bạn cần trang bị kiến thức toán và thông kê. Tuy nhiên bài này mình sẽ giải thích một cách dễ hiểu, mà không dùng
quá nhiều kiến thức toán, hay thống kê.

Cách tốt nhất là bắt đầu với một ví dụ. Ta sẽ giải quyết bài toán "Binary Classification". Trong machine learning thì
"Classification" được xếp vào nhóm Supervised Learning, trong đó dữ liệu được phân chia vào các nhóm xác định trước bởi
Decision Function và hàm này được học qua dataset được gán nhãn trước. Nếu chúng ta chỉ có 2 group cần phân loại, thì bài toán đó là "Binary Classification".

![Data_set](/img/datasets.jpg "Data_set")

### 1. Understanding the Neural Network
![Neural_net](/img/neuralnetworks.jpg "Neural_net")
Hình vẽ trên là một ví dụ về Feedforward Neural network. Dữ liệu được truyền thẳng từ Input vào trong mạng. Trong mạng này thì không có feedback connections cũng như loop trong mạng.

Một mạng thì gồm có Input layer, Output layer và Hidden layer. Thông thường một mạng Neural network sẽ có thể có nhiều Hidden layer. Mỗi một node trong một layer gọi là Neuron.

### 1.1 What is a Neuron
![image-neuron-1.jpg](/img/image-neuron-1.jpg "image-neuron-1")

Hình vẽ trên là ví dụ về Neuron gồm các đầu vào input với các trọng số Wi khác nhau.
Tính tổng các đầu vào sau đó applies một active function để normalize kết quả. Activation function có thể là linear hoặc nonlinear.

### 1.2 Activation function
Trong neural net chúng ta hay gặp các active function sau: 
![Active function.jpg](/img/active-function.jpg "Active function")

### 1.3 Input Layer
Input layer là layer đầu tiên của mạng neural, dùng để input data hoặc feature

 ### 1.4 Output Layer
Đây là layer đưa ra kết quả dự đoán. Với những bài toán khác nhau thì active function ở layer cũng sẽ khác nhau.
Ví dụ với bài toán binary classification chúng ta có output là 0 hoặc 1, do đó active function là sigmoid function.
Với bài toán dạng multiclass classification, active function được sử dụng là Softmax. Trong trường hợp là regression, output
không phải phân chia vào category, ta có thể sử dụng linear unit.

### 1.5 Hidden Layer
Một feedforward network bao gồm một chuỗi các function. Bởi có nhiều hidden layers, chúng ta có thể mô tả hay tính toán
những hàm số phức tạp bằng cách kết hợp các layer và nhiều hàm số đơn giản. Ví dụ chúng ta muốn mô phỏng hàm số mũ 7,
ta có thể sử dụng những hàm đơn giản như square hoặc cube để tạo ra hàm số này. Trong hidden layer, active function được sử dụng phổ biến là hàm ReLU (Rectified Linear Unit).

Việc chọn hidden layer không có quy tắc hay một câu trả lời chính xác. Về cơ bản thì deeper networks có thể học hay mô phỏng những function phức tạp hơn.

### 1.6 How does the network learn?
Dữ liệu từ training sample được đưa vào mạng network, sau đó kết quả output được so sánh với actual output. Sự sai khác này được sử dụng để thay đổi weights của những neutron. Việc tính toán, thay đổi trọng số thông qua thuật toán "Backpropagation".

Backpropagation thường được sử dụng trong các thuật toán gradient để hiệu chỉnh các weight của neutron trong multi-layer neutral networks.

### 2. Why use Hidden Layer?
Để trả lời câu hỏi tại sao chúng ta cần hidden layer, ta có thể sử dụng một công cụ rất trực quan trên web site
http://playground.tensorflow.org để mô phỏng mạng neural và xem tại sao lại cần sử dụng hidden layer.

Giả sử chúng ta có tập dữ liệu với phân bố như sau:
![data-sample.jpg](/img/data-sample.jpg "Data sample")

Với dữ liệu như vậy thì chúng ta cần một decision bound phải có dạng circle, trong trường hợp này linear decision bound không thể phân lớp được dữ liệu.

Chúng ta hãy xem xét các ví dụ dưới đây. Trong hợp không có hidden layer, thì đường phân lớp là linear. Ta có thể thấy rằng, dữ liệu bị phân lớp sai rất nhiều. 
![Hidden-1.jpg](/img/hidden-1.jpg "hidden-1")

Khi chúng ta tăng hidden layer và kết quả như sau:
Với 1 hidden layer, có vẻ như bound decision có vẻ tốt hơn. Với nhũng dữ liệu phức tạp thì việc chúng ta phải tăng thêm hidden layer hoặc tăng thêm neural đều dựa trên thực nghiệm, sẽ không có công thức tổng quát nào để tối ưu việc này.

![Hidden-2.jpg](/img/hidden-2.jpg "hidden-2")

Chúng ta sẽ thử tiếp với 2 hidden layer, và kết quả có vẻ rất khả thi như dưới đây:

![Hidden-3.jpg](/img/hidden-3.jpg "hidden-3")

Như vậy ta có thể thấy rằng, với nhiều hidden layer ta có thể xấp xỉ được những hàm số phức tạp, hay nói cách khác ta có model để biểu diễn mô hình phức tạp.



Bài này mình có tham khảo từ trang web sau:
https://www.learnopencv.com/understanding-feedforward-neural-networks/
