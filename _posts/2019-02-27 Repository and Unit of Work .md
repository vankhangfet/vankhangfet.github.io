---
layout: post
title: Repository 
tags: [Design Pattern]
---

Repository và Unit of Work là những pattern rất hữu dụng. Tuy nhiên cá nhân mình thấy các pattern này có rất nhiều bài viết và cũng không dễ 
để theo dõi. Post này mình sẽ giải thích lại một cách ngắn gọn và dễ hiểu. 

1. Repositoy pattern là gì? Và tại sao nên sử dụng Repository pattern. Hãy xem qua ví dụ sau:

Chúng ta có table Contacts (ID, FirstName, LastName, ContactNumber, Address), và các thao tác với dữ liệu như Delete/Update/Create. 

Việc thao tác với dữ liệu, ta có thể thông qua EF. Chúng ta sẽ gặp những đoạn code sau:

~~~~
public void Create(Contact contact)
{

}
~~~~
