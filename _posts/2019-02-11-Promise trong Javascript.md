---
layout: post
title:  Promise trong JavaScript là gì?
tags: [JS]
---

Trong post này mình sẽ note lại một chút kiến thức về JavaScript, cụ thể là promise trong ES6. Như các bạn đã biết thì ES6 mang đến 
rất nhiều cải tiến, ngoài việc cung cấp cách thức lập trình hướng đối tượng cho JavaScript thì Promise là một pattern rất hay để làm cho code JS trở nên dễ đọc hơn. Vậy Promise làm gì?

Trong JavaScript thì async function và callback là những khái niệm rất quen thuộc, nếu như có nhiều callback lồng vào nhau (nested callback) thì việc xảy ra callback hell rất dễ xảy ra. Hãy thử tưởng tưởng chúng ta phải implement một task vụ sau:

1. cleanRoom();
2. removeGrab();
3. getReward();

1->2->3 kết quả của 1 sẽ là input của 2, kết quả hoàn thành task 2 sẽ là input task3. 1,2,3 đều là async function.

Nếu như implement theo cách thông thường dùng callback thì đoạn code sẽ như sau:

~~~~

function cleanRoom(callback)
{
   // Do something
   var result = Done();
   callback(result);

}

function removeGrab(msg,callback)
{
   // Do something
   var result = Done();
   callback(result)
}

function getReward(msg)
{

}

/* Implement task */

function cleanRoom(function(result1){
                     removeGrab(result1,function(result2){
                                        getReward(result2)
   });
});
~~~~

Các bạn có thể vào link sau: 
[https://jsfiddle.net/vankhangfet/b30f26y7/](https://jsfiddle.net/vankhangfet/b30f26y7/)

Đoạn code trền nhìn khá rổi mắt đúng không? Mặc dù chúng ta đã viết nhỏ các function ra rồi. Hãy thử implement bằng cách sử dụng promise xem sao. Khởi tạo một Promise như sau:

~~~~
let promise = new Promise(function(resolve,reject){
});
~~~~

Ở đây có 2 callback function là resolve và reject. Khi task complete ta gọi hàm resolve, khi fail gọi reject. Về promise thì có rất nhiều bài viết rồi, mình sẽ không giải thích quá nhiều nữa. OK! code thôi. Chúng ta cần modify mỗi function một chút.

~~~~
let cleanRoom = function()
{ 
   var msg = "Clean OK";
   return new Promise(function(resolve,reject){
       resolve(msg);
   });
}

let  removeGrab = function(msg){
   alert(msg);
   var msg2 = "remove OK!";
   return new Promise(function(resolve,reject){
       resolve(msg2)
   });
}

let  getReward = function(msg)
{ 
 alert(msg);
  alert("Get reward");
}

cleanRoom().then(function(msg1){
 return  removeGrab(msg1);
}).then(function(msg2){
   getReward(msg2);
});
~~~~











