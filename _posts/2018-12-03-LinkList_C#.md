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

internal SingleLinkedList
{
   public Node head;
}
~~~~

Với Linked List ta có các thao tác với các phần tử của Linked List như Insert, Delete, Search. 

Insert phần tử vào head

~~~~
internal void InsertFront(SingleLinkedList singlyList, int new_data) {    
    Node new_node = new Node(new_data);    
    new_node.next = singlyList.head;    
    singlyList.head = new_node;    
}    
~~~~

Insert phần từ vào last 

~~~~
internal void InsertLast(DoubleLinkedList doubleLinkedList, int data) {  
    DNode newNode = new DNode(data);  
    if (doubleLinkedList.head == null) {  
        newNode.prev = null;  
        doubleLinkedList.head = newNode;  
        return;  
    }  
    DNode lastNode = GetLastNode(doubleLinkedList);  
    lastNode.next = newNode;  
    newNode.prev = lastNode;  
}  

internal Node GetLastNode(SingleLinkedList singlyList) {  
    Node temp = singlyList.head;  
    while (temp.next != null) {  
        temp = temp.next;  
    }  
    return temp;  
}  
~~~~

Xóa một phần tử trong Linked List 

~~~~
internal void DeleteNodebyKey(SingleLinkedList singlyList, int key)  
{  
    Node temp = singlyList.head;  
    Node prev = null;  
    if (temp != null && temp.data == key) {  
        singlyList.head = temp.next;  
        return;  
    }  
    while (temp != null && temp.data != key) {  
        prev = temp;  
        temp = temp.next;  
    }  
    if (temp == null) {  
        return;  
    }  
    prev.next = temp.next;  
}  
~~~~

Như vậy là chúng ta đã biết một số thao tác với Linked List, tuy nhiên trong thực tế thì Linked List hay được sử dụng như thế nào?

# 4. Linked List và một số ứng dụng

Khi các bạn đã hiểu và cài đặt được kiểu dữ liệu thì Linked List có thể được làm những việc sau:

- Cài đặt một Stack hoặc Queu 

- Cài đặt thao tác Undo như trong Photoshop hoặc Word. 

... Còn rất nhiều ứng dụng nữa, các bạn hãy thử xem sao nhé!
