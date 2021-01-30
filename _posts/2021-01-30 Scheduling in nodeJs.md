---
layout: post
title: Scheduling execution trong Node JS
tags: [Js]
---

NodeJS có khá nhiều thứ đặc biệt, trong đó có một số function khá hay nhưng lại gây ra những điều khó hiểu như: setTimeout, setImmediate và process.nextTick. 
Cả 3 function trên đều có thể được sử dụng để cài đặt schedule trong node js. Tuy nhiên 3 function này lại rất khác nhau. Hãy xem xét ví dụ sau: 

~~~~
setImmediate(() => console.log('Set Immediate'));
setTimeout(() => console.log('Set Timeout'), 0);
process.nextTick(() => console.log('Process NextTick'));
~~~~

Khi check log chúng ta sẽ nhận được kết quả như dưới đây: 

~~~~
> node index.js
Process NextTick
Set Timeout
Set Immediate
~~~~

Để giải thích được kết quả của log trên, chúng ta hãy xem thứ tự của Event Loop:

![Event loop order](/img/event-loop-order.png "Event loop order")
