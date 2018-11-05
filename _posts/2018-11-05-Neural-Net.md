---
layout: post
title: Understanding Feedforward Neural Networks
image: /img/neuralnetworks.jpg
tags: [Machine learning]
---

Bài này mình có tham khảo từ trang web sau:
https://www.learnopencv.com/understanding-feedforward-neural-networks/

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
