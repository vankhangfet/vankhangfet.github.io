
---
layout: post
title: View model trong kiến trúc MVVM
tags: [DESIGN]
---

Những ai đã từng làm việc với kiến trúc MVVM sẽ không xa lạ với Viewmodel. ViewModel là một thành phần có ảnh 
hưởng rất lớn tới kiến trúc MVVM. Tuy nhiên chính ViewModel cũng là thanh phần gây ra khá nhiều hiểu lầm 
cho các bạn lập trình viên. Trong post này mình sẽ thảo luận về View Model, triển khai View Model đúng với kiến trúc MVVM. 

Tư tưởng của ViewModel

Trong kiến trúc MVVM, rất khó để chúng ta thực hiện UT cho layer View. Do đó mặc nhiên việc triển khai UT sẽ 
được thực hiện tại layer ViewModel.

Viewmodel nên được thiết kế một cách abstraction. ViewModel sẽ không thể hiện sự liên quan tới một menu hay một
button cụ thể nào trên UI (View layer). ViewModel có nhiệm vụ thể hiện data sẽ được xử lý và có liên quan giữa các thành phần trên UI như thế nào.
