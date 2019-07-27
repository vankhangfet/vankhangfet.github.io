---
layout: post
title: Làm quen với React
tags: [JS]
---

Mặc dù React là một thư viện JavaScript đã được release và các lập trình viên làm việc khá lâu rồi. Nhưng hôm nay mình mới có cơ hội được
làm quen và thực hành với React. 

1. Lý do tại sao mình làm việc với React?
Thực ra thì do project yêu cầu, nên mình phải tìm hiểu. Như các bạn đã biết thì hiện nay có rất nhiều các thư viện JavaScript, do đó nếu
như cái nào bạn cũng học thì rất là khó có thời gian phải không nào? Ok ta sẽ xem React có những gì và làm được gì?

Sơ qua về React là thư viện javascript do Facebook phát triển. React dùng để xây dựng nên những thành phần UI của trang web. Như các bạn
đã biết thì Single page là một web application khá phổ biến hiện nay. Để thuận tiện cho việc tổ chức, tái sử dụng các thành phần (Component) thì React sinh ra để làm như vậy. Khi làm việc với React các bạn sẽ được nghe thấy rất nhiều đền Component. 

Ví dụ một trang web có Header, Footer, etc. Thì Header hay Footer chính là một Component theo cách nhìn của React. Và các Component có thể tương tác với nhau thông qua các Props. 

Hãy xem một ví dụ Hello World với React JS 

Code JS: 
~~~~
ReactDOM.render(
  <h1>Hello, world!</h1>,
  document.getElementById('root')
);
~~~~
HTML: 
~~~~
<div id="root"></div>
~~~~

Chỉ với đoạn code đơn giản như trên, thẻ div sẽ hiển thị câu "Hello, world!". Chúng ta sẽ xem chi tiết xem Component là gì?
![component](https://cdn-images-1.medium.com/max/800/1*N2KU7pOcwZwKeOi3B-YBLQ.png "component")





