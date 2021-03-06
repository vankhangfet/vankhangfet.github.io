---
layout: post
title: Note about CQRS 
tags: [DDD]
---

Trong thời gian gần đây tôi và anh bạn đồng nghiệp có disscuss về CQRS và cách thức triển khai CQRS. Có một số nhầm lẫn về CQRS. 
Nhiều bạn quan niệm rằng CQRS là một kiến trúc (architecture), nhưng nó không phải. CQRS đơn giản chỉ là một pattern. CQRS không đề cập đến vấn đề 
đồng nhất dữ liệu, không phải event, cũng như message. Về cơ bản CQRS cũng không phải là việc chia model read/write.

CQRS Command and Query Responsibility Segregation

Cài đặt CQRS đơn giản chỉ là tạo ra 2 thực thể. Việc chia làm 2 thực thể này phụ thuộc vào method đó là query hay command. Khi nói đến CQRS nghĩa là chúng ta nói đến
việc apply CQRS pattern nên boundary service. Hãy xem xét ví dụ sau:

~~~~
CustomerService

void MakeCustomerPreferred(CustomerId)
Customer GetCustomer(CustomerId)
CustomerSet GetCustomersWithName(Name)
CustomerSet GetPreferredCustomers()
void ChangeCustomerLocale(CustomerId, NewLocale)
void CreateCustomer(Customer)
void EditCustomerDetails(CustomerDetails)
~~~~

Khi apply CQRS, chúng ta sẽ có 2 services sau:

~~~~
CustomerWriteService

void MakeCustomerPreferred(CustomerId)
void ChangeCustomerLocale(CustomerId, NewLocale)
void CreateCustomer(Customer)
void EditCustomerDetails(CustomerDetails)
~~~~

~~~~
CustomerReadService

Customer GetCustomer(CustomerId)
CustomerSet GetCustomersWithName(Name)
CustomerSet GetPreferredCustomers()
~~~~

Cách tiếp cận đơn giản là như vậy. Việc chia tách service này mang đến cho kiến trúc, ứng dụng của chúng ta rất nhiều điều thú vụ và khả năng mở rộng service.
Ví dụ chúng ta có thể mở rộng service query một cách dễ dàng.




