---
layout: post
title: How to get a cup of coffee - API design?
tags: [DESIGN]
---

Rest full - API đã rất quen thuộc với các bạn làm backend. Tuy nhiên để hiểu đúng và làm đúng thì là một chuyện khác. Nhân cơ hội đọc được bài 
"https://www.infoq.com/articles/webber-rest-workflow/", mình note lại vài điểm chú ý trong thiết kế API. Mình khuyên các bạn nên đọc bài nguyên gốc, có khá nhiều điều thú 
vị trong bài viết tiếng anh.

Trong bài này có đề cập đến vấn đề thiết kế API, phục vụ cho việc khách hàng order coffee. Thử tượng tượng chúng ta sẽ thiết kế API cho Starbucks. Hãy bắt đầu với work flow và
state machine.

![Customer state machine](https://res.infoq.com/articles/webber-rest-workflow/en/resources/image1.jpg)

Đây là một flow rất phổ biến, customer có thể order, thay đổi order và thực hiện thanh toán. Tiếp đến là flow của người pha chế 


![Barista's state machine](https://res.infoq.com/articles/webber-rest-workflow/en/resources/image2.jpg)

Người pha chế sẽ nhận order, thực hiện pha chế. Ok!, với 2 state machine cơ bản như vậy, chúng ta đã hiểu được flow làm việc của hệ thống, giờ là lúc thiết kế API. 

Với customer, thì customer sẽ cần order đồ uống "Coffee" 
![Customer order](https://res.infoq.com/articles/webber-rest-workflow/en/resources/image3.jpg)

Để thực hiện order này, đơn giản là chúng ta sẽ thực hiện một "POST" request, và endpoint cho việc order này sẽ như sau: 
"http://starbucks.example.org/order."

![Ordering coffee](https://res.infoq.com/articles/webber-rest-workflow/en/resources/image4.jpg)
