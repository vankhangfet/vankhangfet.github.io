---
layout: post
title: Inversion of Control, DI là gì?
tags: [.Net]
---
Mình nhận thấy có khá nhiều bạn gặp khó khăn trong việc hiểu và implment các khái niệm như DI, IoC. Post này mình sẽ tìm hiểu làm thế nào để triển khai IoC. Bài này mình dịch và tham khảo site sau: https://www.tutorialsteacher.com/ioc/inversion-of-control. Cá nhân mình thấy bài viết khá dễ hiểu và có tính thực hành cao. Để triển khai IoC, chúng ta folow theo step sau:

![ioc-step](https://www.tutorialsteacher.com/Content/images/ioc/ioc-step1.png "IoC steps")

Trước khi đi vào chi tiết thì chúng ta cần làm rõ một số điểm sau. IoC là design principle, nó không phải là một Pattern. 
IoC giúp chúng ta thiết kế chương trình loosely copupled. làm cho chương trình trở nên dễ test, mở rộng và bảo trì. 

![ioc-dip](https://www.tutorialsteacher.com/Content/images/ioc/principles-and-patterns.png "IoC&DIP")

Tuy nhiên để làm cho chương trình loosely, chúng ta phải kết hợp cả IoC và DIP chứ không chỉ áp dụng mỗi IoC. 

Chúng ta hãy xem những kiến trúc phổ biến như hình dưới:

![demo](https://www.tutorialsteacher.com/Content/images/ioc/demo-architecture.png "demo")

Trong kiến trúc N-tier, ta sẽ tập trung vào BusinessLogic class và  DataAccess class để hiểu về IoC. Ví dụ chương trình được thiết kễ như sau:

~~~~
public class CustomerBusinessLogic
{
    DataAccess _dataAccess;
    public CustomerBusinessLogic()
    {
        _dataAccess = new DataAccess();
    }
    public string GetCustomerName(int id)
    {
        return _dataAccess.GetCustomerName(id);
    }
}

public class DataAccess
{
    public DataAccess()
    {
    }
    public string GetCustomerName(int id) {
        return "Dummy Customer Name"; // get it from DB in real app
    }
}
~~~~

Về mặt thiết kế, code như vậy có vẻ ngắn gọn, tuy nhiên lại có một vấn đề là class CustomerBusinessLogic bị gắn chặt vào class DataAccess. 
1. Giả sử nếu như chương trình cần kết nỗi với nhiều data source khác nhau để lấy thông tin User thì chúng ta sẽ phải sửa 
chữa class DataAccess này. 

2. Hoặc đơn giản như việc thay đổi class name cũng sẽ dẫn tới việc thay đổi rất nhiều chỗ. Về cơ bản thì đây là một thiết kế không tốt, khó mở rộng. 

Để giải quyết vấn đề trên chúng ta cần kết hợp IoC và DIP. Chú ý là IoC là tư tưởng thiết kế do đó chúng ta có rất nhiều cách triển khai, bạn có thể free design. 
Như mình để cập ở trên chúng ta sẽ apply từng step để imporve thiết kế trên:

Step 1: Create Simple Factory Class 
~~~~
public class DataAccessFactory
{
    public static DataAccess GetDataAccessObj() 
    {
        return new DataAccess();
    }
}
~~~~
Lúc này việc get object Data access sẽ thông qua class DataAccessFactory

~~~~
public class CustomerBusinessLogic
{
    public CustomerBusinessLogic()
    {
    }
    public string GetCustomerName(int id)
    {
        DataAccess _dataAccess =  DataAccessFactory.GetDataAccessObj();
        return _dataAccess.GetCustomerName(id);
    }
}
~~~~

Đó là tư tưởng sử dụng IoC, thay vì trực tiếp tạo ra object DataAccess chúng ta dùng class DataAccessFactory để tạo ra object này. 
Tuy nhiên để hoàn toàn loosely couple thì chúng ta phải kết hợp DIP nữa. 

Nhắc lại một chút DIP:
1. High-level modules should not depend on low-level modules. Both should depend on the abstraction.
2. Abstractions should not depend on details. Details should depend on abstractions.

Nguyên tắc số 1 nghe có vẻ dễ hiểu, còn số 2 khá là khó hiểu đúng không?

Abstraction là trừu tượng, một cái gì đó không cụ thể. Với ví dụ ở trên thì class CustomerBusinessLogic là cái rất cụ thể. Vậy nguyên tắc số 2 đề cập đến việc sử dụng interface và Abstraction class 

Ok! áp dụng DIP vào ví dụ trên. Chúng ta sẽ tạo ra một Interface như sau:
~~~~
public interface ICustomerDataAccess
{
    string GetCustomerName(int id);
}
~~~~
Và thay đổi class DataAccess và CustomerBusinessLogic class như sau:
CustomerDataAccess
~~~~
public class CustomerDataAccess: ICustomerDataAccess
{
    public CustomerDataAccess()
    {
    }
    public string GetCustomerName(int id) {
        return "Dummy Customer Name";        
    }
}
~~~~
CustomerBusinessLogic
~~~~
public class CustomerBusinessLogic
{
    ICustomerDataAccess _custDataAccess;

    public CustomerBusinessLogic()
    {
        _custDataAccess = DataAccessFactory.GetCustomerDataAccessObj();
    }

    public string GetCustomerName(int id)
    {
        return _custDataAccess.GetCustomerName(id);
    }
}
~~~~
