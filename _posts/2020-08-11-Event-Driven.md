---
layout: post
title: Event-Driven là gì?
tags: [DESIGN]
---
Trong quá trình làm việc, mình hay nghe các đồng nghiệp nhắc tới kiến trúc "Event-Driven". Tuy nhiên khi nhắc đến khái niệm này thì 
có nhiều điểm khác biệt. Post này mình note lại một số điểm về chính về Event-Driven.

1. Event Notification 
Đây là pattern khá phổ biến. Điểm chính của Event Notification là source system nơi phát sinh event sẽ không cần phải quan tâm tới service sẽ 
xử lý event và response event này. Pattern này giúp chúng chia tách được business giữa modul phát sinh event và module xử lý event.
Tuy nhiên vấn đề phát sinh là chúng ta sẽ khó để nhìn được toàn bộ flow của hệ thống. Việc debug và thay đổi flow của application cũng sẽ trở nên khó khăn hơn.
Ngoài ra điểm cần chú ý nữa là một event không nên mang quá nhiều data, thông thường event gồm thông tin về id,và linkback lại sender để receiver có thể cần 
gửi tới sender để nhận thêm thông tin.


2. Event-Carried State Transfer


3. Event-Sourcing
Ý tưởng chính của event sourcing đó là khi chúng ta thay đổi state của system, chúng ta sẽ record lại sự thay đổi này như một event và chúng ta 
có thể rebuild lại được trạng thái của system bằng cách xử lý event tại bất cứ thời điểm nào trong tương lai.
