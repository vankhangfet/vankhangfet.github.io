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
~~~~

Tuy nhiên mình không khuyến khích làm cách này, vì nó khá khó bảo trì và quản lý scope của các biến. 

Solution 2:

