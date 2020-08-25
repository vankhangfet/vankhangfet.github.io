---
layout: post
title: Dependency with Ninject 
tags: [Design Pattern]
---
Như các bạn đã biết thì Dependency Injection là một mẫu thiết kế để giảm sự phụ thuộc của các module. Có rất nhiều thư viện hỗ trợ chúng ta triển khai việc này. 
Ninject là một thư viện khá hay, và dễ sử dụng. Hãy cùng xem ví dụ sau và các áp dụng Ninject như thế nào?

Chúng ta bắt đầu với ví dụ send email: 

~~~~
public interface IConfirmationMessageSender
{
   void Send(string message, string email);
}


public class EmailMessageSender: IConfirmationMessageSender
{   
   public void Send(string message, string email)
   { 
     Console.WriteLine("Email recipient={0} : data={1}", email,message);
   }
}

public class MessageSender
{ 
   // a lot of complicated stuff here :)
   // ..
   // ..
  
   public void SendMessage(string message, string email)
   {
     EmailSender emailSender = new EmailSender(); 
     emailSender.Send(message,recipient); 
   } 

   // ..
   // ..

}

class Program
{   
   void Main(string[] args)
   {
      MessageSender messageSender = new MessageSender();
      messageSender.SendMessage("Some text","test@gmail.com"); 
   }
}
~~~~

Đoạn code trên khá dễ hiểu, tuy nhiên lại có một số vấn đề về như sau:

1. Extensible isssue: Nếu như trong quá trình phát triển, chúng ta cần thêm một channel để gửi thông tin ví dụ SMS thì việc thay đổi là không dễ dàng. 

2. Coupling issue: Trong ví dụ này MessageSender class sẽ bị phụ thuộc trực tiếp vào EmailSender class.

3. Testability issue: Nếu giả sử bạn cần test class MessageSender độc lập thì nó vi phạm tư tưởng của Unit testing đó là việc có thể tiến hành test các 
method hay component một cách độc lập

Để giải quyết vấn đề trên thì đây là lúc chúng ta nghĩ đến Dependency Injection. Mục đích là làm giảm sự phụ thuộc giữa các class, component. 

Hãy thử triển khai thêm dịch vụ gửi SMS và kiến trúc lại hệ thống:

~~~~
public interface IConfirmationMessageSender
{
   void Send(string message, string recipient);
}

public class EmailMessageSender: IConfirmationMessageSender
{   
   public void Send(string message, string recipient)
   { 
     Console.WriteLine("Email recipient={0} : data={1}", recipient,message);
   }
}

public class SMSMessageSender: IConfirmationMessageSender
{   
   public void Send(string message, string recipient)
   { 
     Console.WriteLine("SMS recipient={0} : data={1}", recipient,message);
   }
}

public class MessageSender
{
 IConfirmationMessageSender _messageSender = null;

 public MessageSender(IConfirmationMessageSender messageSender)
 {
   _messageSender = messageSender;
 }

 public void SendMessage(string message, string recipient) 
 { 
   _messageSender.Send(message,recipient); 
 } 
}

~~~~
Và sử dụng SMS sensder như sau: 
~~~
class Program
{   
   void Main(string[] args)
   {
      IConfirmationMessageSender confirmationMessage = new SMSMessageSender();
      MessageSender messageSender = new MessageSender(confirmationMessage); 
      messageSender.SendMessage("Some text","123456789");
      Console.ReadKey(); 
   } 
}
~~~
Với việc tổ chức code lại như trên chúng ta đã giải quyết được issue như: 

1. Extension: Nếu như cần thay đổi cách thức để gửi message, chúng ta có thể dễ dang thay đổi hay mở rộng. Và quan trọng là việc thay đổi không vi phạm nguyên tắc 
Open-Close principle. 

2. Testability: chương trình cho phép ta có thể test class MessageSender với bất cứ kiểu communication nào (EmailSender, SMSSender, etc.)

3. Tight coupling: sự phụ thuộc giữa MessageSender và EmailMessageSender class đã được giải quyết.

Tuy nhiên chúng ta có thể làm cho việc triển khai dễ dàng hơn bằng cách sử dụng Ninject Framework. Ở đây chúng ta sẽ không đi quá chi tiết vào Ninject mà chỉ 
xem xét cách ứng dụng Framework này như thế nào: 

Step1: chúng ta sẽ định nghĩa một Binding class như sau: 
~~~~
using Ninject;
using Ninject.Modules;
public class Bindings: NinjectModule
{   
   public override void Load()
   { 
     Bind<IConfirmationMessageSender>().To<SMSMessageSender>(); 
   } 
}
~~~~
Ý tưởng ở đây là khai báo để Ninject biết mapping giữa interface và một implementation cụ thể. Nếu như muốn thay đổi cách thức gửi message chúng ta chỉ cần thay đổi 
mapping, mà gần như không phải thay đổi code trong hệ thống. Great!!!!!!!!!!!!!!!

Step2: Chúng ta sẽ khởi tạo kernerl entity để mapping giữa interface và implementation. 
~~~~
IKernel kernel = new StandardKernel();
kernel.Load(Assembly.GetExecutingAssembly());
~~~~

Và việc cuối cùng là chúng ta sử dụng để implement như sau: 
~~~~
IConfirmationMessageSender confirmationMessage = new kernel.Get<IConfirmationMessageSender>(); 
MessageSender messageSender = new MessageSender(confirmationMessage); 
messageSender.SendMessage("Some text","123456789");
~~~~

Final code sẽ như sau: 

~~~~
using Ninject;
using Ninject.Modules;
public interface IConfirmationMessageSender
{
   void Send(string message, string recipient);
}
public class EmailMessageSender: IConfirmationMessageSender
{   
   public void Send(string message, string recipient)
   { 
     Console.WriteLine("Email recipient={0} : data={1}", recipient,message);
   }
}
public class SMSMessageSender: IConfirmationMessageSender
{   
   public void Send(string message, string recipient)
   { 
     Console.WriteLine("SMS recipient={0} : data={1}", recipient,message);
   }
}
public class MessageSender
{
 IConfirmationMessageSender _messageSender = null;

 public MessageSender(IConfirmationMessageSender messageSender)
 {
   _messageSender = messageSender;
 }

 public void SendMessage(string message, string email) 
 { 
   _messageSender.Send(message,email); 
 } 
}

public class Bindings: NinjectModule
{   
   public override void Load()
   { 
     Bind<IConfirmationMessageSender>().To<SMSMessageSender>(); 
   } 
}
class Program
{   
   void Main(string[] args)
   {
      IKernel kernel = new StandardKernel();
      kernel.Load(Assembly.GetExecutingAssembly());
      IConfirmationMessageSender confirmationMessage = kernel.Get<IConfirmationMessageSender>(); 
      MessageSender messageSender = new MessageSender(confirmationMessage); 
      messageSender.SendMessage("Some text","123456789");
      Console.ReadKey();
   } 
}
~~~~





