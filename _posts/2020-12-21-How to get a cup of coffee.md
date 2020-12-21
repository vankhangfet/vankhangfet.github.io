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

Giả sử customer thực hiện một order như sau: 

![Ordering coffee1](https://res.infoq.com/articles/webber-rest-workflow/en/resources/code1.jpg)

Khi thực hiện order này thì "Starbucks service" sẽ thực hiện tạo một resource và response lại customer thông tin order này trong response. Ngoài ra service có thể response cho 
người dùng thông tin cần thiết cho việc thực hiện thanh toán. Response sẽ có dạng như sau:

![Ordering coffee2](https://res.infoq.com/articles/webber-rest-workflow/en/resources/code2.jpg)

Http code 201 cho chúng ta biết Starbucks đã nhận order thành công. Ngoài ra chúng ta còn có thể có các HTTP status khác dưới đây

~~~~
We've already seen that the 201 Created status code indicates the successful creation of a resource. We'll need a handful of other useful codes both for this example and for Web-based integration in general:
200 OK - This is what we like to see: everything's fine; let's keep going. 201 Created - We've just created a resource and everything's fine.
202 Accepted - The service has accepted our request, and invites us to poll a URI in the Location header for the response. Great for asynchronous processing.
303 See Other - We need to interact with a different resource. We're probably still OK.
400 Bad Request - We need to reformat the request and resubmit it.
404 Not Found - The service is far too lazy (or secure) to give us a real reason why our request failed, but whatever the reason, we need to deal with it.
409 Conflict - We tried to update the state of a resource, but the service isn't happy about it. We'll need to get the current state of the resource (either by checking the response entity body, or doing a GET) and figure out where to go from there.
412 Precondition Failed - The request wasn't processed because an Etag, If-Match or similar guard header failed evaluation. We need to figure out how to make forward progress.
417 Expectation Failed - You did the right thing by checking, but please don't try to send that request for real.
500 Internal Server Error - The ultimate lazy response. The server's gone wrong and it's not telling why. Cross your fingers…
~~~~

Tuy nhiên trong thực tế không phải lúc nào customer cũng chỉ có một order, và họ cũng có thể thay đổi order 


![Ordering coffee3](https://res.infoq.com/articles/webber-rest-workflow/en/resources/image5.jpg)

Tuy nhiên để chắc chắn rằng chúng ta có thể thay đổi order thì thật may mắn là HTTP hỗ trợ method "OPTIONS" để làm việc này

~~~~
Request:
OPTIONS /order/1234 HTTP 1.1 Host: starbucks.example.org
Response:
200 OK Allow: GET, PUT
~~~~
Chúng ta có thể thấy là việc update order vẫn là hợp lệ và được hồ trợ bởi method "PUT", tất nhiên việc lấy thông tin order được hỗ trợ bởi method "GET". 
Nếu chúng ta thử thay đổi order với "PUT" thì response sẽ như sau: 
~~~~
Request: 
PUT /order/1234 HTTP 1.1 Host: starbucks.example.com Expect: 100-Continue
Response:
100 Continue
~~~~
Trong trường hợp, nếu như không thể thay đổi được order thì response sẽ là "417 Expectation Failed". Giả sử chúng ta thay đổi order như sau với "PUT"
![Ordering coffee4](https://res.infoq.com/articles/webber-rest-workflow/en/resources/code3.jpg)

Khi order được thay đổi, service sẽ response thông tin của order (new resource) như sau:
![Ordering coffee5](https://res.infoq.com/articles/webber-rest-workflow/en/resources/code4.jpg)



