---
layout: post
title:  Promise trong JavaScript là gì?
tags: [JS]
---

Trong post này mình sẽ note lại một chút kiến thức về JavaScript, cụ thể là promise trong ES6. Như các bạn đã biết thì ES6 mang đến 
rất nhiều cải tiến, ngoài việc cung cấp cách thức lập trình hướng đối tượng cho JavaScript thì Promise là một pattern rất hay để làm cho code JS trở nên dễ đọc hơn. Vậy Promise làm gì?

Trong JavaScript thì async function và callback là những khái niệm rất quen thuộc, nếu như có nhiều callback lồng vào nhau (nested callback) thì việc xảy ra callback hell rất dễ xảy ra. Hãy thử tưởng tưởng chúng ta phải implement một task vụ sau:

1. cleanRom();
2. removeGrab();
3. getReward();

