---
layout: post
title: Implement stack trong JavaScript
tags: [JS]
---

Javascript là một ngôn ngữ rất thú vị, chúng ta có thể làm được rất nhiều thứ với JS. Hiện nay có khá nhiều framework với JS, tuy nhiên bài này mình không có ý định làm việc với một framework cụ thể nào, mà chỉ xem lại cách thức implement một class trong js như thế nào và cài đặt một stack bằng Js. 

Về cơ bản một Stack sẽ hỗ trợ nhừng method sau:

~~~~
class Stack
{
   push(element)
   pop()
   peek()
   isEmpty()
   print()

}
~~~~

Stack làm việc theo nguyên tắc LIFO (Last in first out), ở đây có method peek() nghĩa là lấy ra phần tử top most trong stack, nhưng không xóa bỏ phần tử đó trong stack. OK! chúng ta hãy implement như sau:
~~~~
class Stack{
	
	constructor()
	{
		// Array is used to implement stack
		this.items = [];
	}
	
	// Function 
	// push(item)
	// pop()
	// peek()
	// isEmpty()
	// printStack()
	
	push(element)
	{
		
		this.items.push(element);
	}
	
	pop()
	{
		if(this.items.length == 0)
			return "Underflow"
		return this.items.pop();
		
	}
	
	peek()
	{
		// return the top most element from stack 
		// but doen't delete it
		return this.items[this.items.length -1];
		
	}
	
	isEmpty()
	{
		
		return this.items.length == 0;
	}
	
}
~~~
// How to use stack 
~~~
var stack = new Stack();
// Adding element to the stack

stack.push(10);
stack.push(20);
stack.push(30);
~~~~

Cài đặt stack trong JS khá đơn giản phải không? Stack là một cấu trúc dữ liệu rất hay dùng. Hy vọng các bạn áp dụng thành công cấu trúc dữ liệu này.
