---
layout: post
title: Scheduling execution trong Node JS
tags: [Js]
---

NodeJS có khá nhiều thứ đặc biệt, trong đó có một số function khá hay nhưng lại gây ra những điều khó hiểu như: setTimeout, setImmediate và process.nextTick. 
Cả 3 function trên đều có thể được sử dụng để cài đặt schedule trong node js. Tuy nhiên 3 function này lại rất khác nhau. Hãy xem xét ví dụ sau: 

Chúng ta có một đoạn code index.js như sau:
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

process.nextTick - callback được enqueue(đưa vào) nextTickQueue. Queue này sẽ được hủy đi khi block code hiện tại được kết thúc. Sau đó việc điều khiển được trả lại event loop

OK! giờ chúng ta hãy thử dùng các định nghĩa trên để giải thích kết quả log

1. Entry script(index.js) được thực thi.

2. nextTickQueu được xử lý. process.nextTick enqueue callback, và sau đó call back được thực thi 

3. Event Loop resumes. 

4. Timer phase detect một timer với delay 0ms được được set bởi setTimout. Lúc này timer callback sẽ được enqueu (đưa vào quêu). 

5. Event lopp chuyển qua poll phase. Timer callback sẽ được thực dequeue và thực hiện.

6. Poll queue là empty, khi có cài đặt callback trong setImmediate thì evet lopp sẽ chuyển qua check phase. 

7. Call back trong setImmediate được thực hiện

8. Event loop được restart. Nếu như không có timer hoặc I/O process nào đang pending thì kết thúc process.

Vậy các sheduling function được sử dụng trong những trường hợp nào?

- setTimeout : được dùng để schedule cho một function sẽ được thực thi sau khi delay milliseconds


