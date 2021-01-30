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

Chúng ta hãy xem thứ tự của Event Loop sau:

![Event loop order](/img/event-loop-order.png "Event loop order")

setTimeout - sẽ được schedule trong timers, và thực thi ngay lúc đầu trong quá poll phase

setImmeidate - được thi trong check phase khi poll phase không tác vụ. Poll phase là phase mà 99% callback trong node js được thực thi. Hay nói cách khác thì setImmediate được dealy cho tới khi event queue là empty. 

process.nextTick - callback được enqueue từ nextTickQueue. Queue này sẽ được hủy đi khi block code hiện tại được kết thúc. 

OK! giờ chúng ta hãy thử dùng các định nghĩa trên để giải thích kết quả log



