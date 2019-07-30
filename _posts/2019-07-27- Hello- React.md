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
Đây là một ví dụ về class component. Mọi class Component đều kế thừa từ React.Component. Bản thân component là có các thành phần như 
function, handler, state và props. Với Component, chúng ta sẽ phải làm quen với State và Props.

![state&Props](https://i.stack.imgur.com/wqvF2.png "State & Props")

Để cho dễ hiểu State và Props ta xem ví dụ sau: Chúng ta muốn tạo ra một component là Label, với thuộc tính là text có thể thay đổi
được. Khi click button thì text hiển thị số lần click ( 1 click, 2 click,...). Ở ví dụ dưới chúng ta sẽ biết được cách truyền value giữa các Component như thế nào?

1. Parent to Child (using props)
   App
      └── Parent
          ├── Child1
          └── Child2
2. Child to Parent (using callback)
   
3. Between Siblings (using redux)

Ở đây mình sẽ demo Button -> Content -> Label. Mình sẽ viết về Redux sau. 


~~~~
class App extends React.Component {
   constructor()
   {
	   super();
	   this.state = {
          message: "This is parrent",
          value: 0 
		  
	   }
	   
	   this.callbackFunction = this.callbackFunction.bind(this);
   }   
   
   callbackFunction(childData)
   {
      this.setState({value:childData});

   }
	
   render() {
      return (
         <div>
          <p> Hello React </p>
          <Button parrentCallBack ={this.callbackFunction}></Button>
           <Label dataFromParent = {this.state.value}> </Label>
         </div>
      );
   }
}

class Label extends React.Component
{

  constructor()
  {
    super();

  }
  
  render()
  {

     return (
        <div>Click: {this.props.dataFromParent}</div>
     );
  }
}


class Button extends React.Component
{

   constructor()
   {  
      super();
      this.state = {counter: 1};
      this.onClick = this.onClick.bind(this);

   }

   onClick()
   {
      this.setState({counter: this.state.counter +1});
      this.props.parrentCallBack(this.state.counter);

   }
   
   render()
   {
      return (
          <button onClick={this.onClick}>Increase</button> 
      );
   }

}
~~~~

Để làm việc dễ hơn thì Debug là một phần rất quan trọng, hãy dùng React Extension sau: 
https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi?hl=en

OK, run code. Mình sẽ có kết quả như dưới. Mỗi khi click button thì giá trị sẽ được update và hiển thị lên text.




