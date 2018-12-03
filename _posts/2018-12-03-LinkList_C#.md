---
layout: post
title: Linklist trong C#
tags: [.Net]
---

Linked List là một cấu trúc dữ liệu mà bạn nào học C++ cũng sẽ gặp. Tuy nhiên ứng dụng và cách cài đặt thì không nhiều bạn biết, mình cũng thấy
khá bất ngờ khi một số bạn không biết cách cài đặt kiểu dữ liệu này. Post này mình sẽ thử xem có bao nhiêu kiểu Linked List ,
cài đặt cấu trúc dữ liệu này bằng C#. Nếu chỉ cài đặt không thì các bạn sẽ hỏi cấu trúc dữ liệu này là gì? Ứng dụng thế nào? Có ưu nhược
điểm gì khi dùng kiểu dữ liệu này không? Chúng ta sẽ giải quyết từng vấn đề dưới đây.

# 1. Linked List là gì?
Linked List là kiểu dữ liệu gồm một list các node. Node có gồm có data và adress (adress: chứa địa chỉ node tiếp theo.)
Node đầu tiên trong node gọi là Head
![Linked List](https://csharpcorner-mindcrackerinc.netdna-ssl.com/article/linked-list-implementation-in-c-sharp/Images/LL_1.png "Linked List")

# 2. Có những kiểu Linked List nào?

Single Linked List:

![Single Linked List](https://csharpcorner-mindcrackerinc.netdna-ssl.com/article/linked-list-implementation-in-c-sharp/Images/LL_2.png "Single Linked List")

Double Linked List: 

![Double Linked List](https://csharpcorner-mindcrackerinc.netdna-ssl.com/article/linked-list-implementation-in-c-sharp/Images/LL_4.png "Double Linked List")

Circula Linked List:

![Circula](https://csharpcorner-mindcrackerinc.netdna-ssl.com/article/linked-list-implementation-in-c-sharp/Images/LL3.png "Circula")


# 3. Cài đặt một Linked List như thế nào? 

Mình code C#, nên sẽ cài đặt bằng ngôn ngữ này. Theo mình ngôn ngữ chỉ là công cụ, khi đã hiểu bản chất thì việc cài đặt bằng ngôn ngữ khác cũng không phải là vấn đề quá khó.

~~~~
internal class Node
{
   public int Data;
   public Node Next;
   
   public Node(int val)
   {
      Data = val;
      Next = null;
   }

}
~~~~


