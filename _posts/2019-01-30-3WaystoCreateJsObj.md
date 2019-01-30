---
layout: post
title:  3 cách việt class trong JavaScript
tags: [JS]
---

Như mình đã viết trong post trước thì Js là một ngôn ngữ thú vị. Tuy nhiên nó lại không chặt chẽ, do đó có quá nhiều cách viết hay triển khai một class. Post này mình sẽ giới thiệu với bạn 3 cách để implement một class. 

Trong js thì ngay cả một class cũng là một function. Chúng ta sẽ tiếp cận cách thức triển khai một class như sau:

Solution 1: 
~~~~
function Apple(type)
{
    this.type = type;
    this.color = color;
    this.getInfo = getAppleInfor;

}

function getAppleInfor()
{
   return this.color + "" + this.type;
}

// How to use

var apple = new Apple("MAC");
apple.color = "Black";
alert(apple.getInfo);
~~~~

Tuy nhiên mình không khuyến khích làm cách này, vì nó khá khó bảo trì và quản lý scope của các biến. 

Solution 2:

Chúng ta cần cải tiến một chút, hãy đưa function vào trong class Apple này.

~~~~
function Apple(type)
{
   this.type = type;
   this.color = color;
   this.getInfo = function()
   {
     return this.type + " " + this.color;
   }
}
~~~~

Solution 3: 

Add method vào class thông qua prototype.

~~~~
function Apple(type)
{
   this.type = type;
   this.color = color;
}

Apple.prototype.getInfo = function {
  return this.type + "" + this.color;
}

~~~
