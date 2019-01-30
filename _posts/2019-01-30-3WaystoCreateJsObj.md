---
layout: post
title:  3 cách để tạo class trong JavaScript
tags: [JS]
---

Như mình đã viết trong post trước thì Js là một ngôn ngữ thú vị. Tuy nhiên nó lại không chặt chẽ, do đó có quá nhiều cách viết hay triển khai một class. Post này mình sẽ giới thiệu với bạn 3 cách để implement một class. 

Trong js thì ngay cả một class cũng là một function. Chúng ta sẽ tiếp cận cách thức triển khai một class như sau:

Solution 1: 
~~~~
function Apple(type)
{
    this.type = type;
    this.color = "red";
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
   this.color = "red";
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
   this.color = "red";
}

Apple.prototype.getInfo = function {
  return this.type + "" + this.color;
}

~~~

Như vậy là các bạn đã biết cách tạo class sử dụng 3 cách trên. Vậy muốn kế thừa class thì ta làm thế nào? Giả sử chúng ta có class Hero và Mage. Class Mage sẽ kế thừa class Hero

~~~~
function Hero(name, level) {
    this.name = name;
    this.level = level;
}

// Adding a method to the constructor
Hero.prototype.greet = function() {
    return this.name ;
}

// Creating a new constructor from the parent
function Mage(name, level, spell) {
    // Chain constructor with call
    Hero.call(this, name, level);
    this.spell = spell;
}
~~~~
Khá đơn giản phải không? Hy vọng post này sẽ giúp bạn dễ dàng làm việc hơn với Js!

