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





