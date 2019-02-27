---
layout: post
title: Repository 
tags: [Design Pattern]
---

Repository và Unit of Work là những pattern rất hữu dụng. Tuy nhiên cá nhân mình thấy các pattern này có rất nhiều bài viết và cũng không dễ 
để theo dõi. Post này mình sẽ giải thích lại một cách ngắn gọn và dễ hiểu. 

1. Repositoy pattern là gì? Và tại sao nên sử dụng Repository pattern. Hãy xem qua ví dụ sau:

Chúng ta có table Contacts (ID, FirstName, LastName, ContactNumber, Address), và các thao tác với dữ liệu như Delete/Update/Create. 

Việc thao tác với dữ liệu, ta có thể thông qua EF. Chúng ta sẽ gặp những đoạn code sau:

~~~~
public void Create(Contact contact)
{
   Contact contact = db.Contacts.AddObject(contact);
   db.SaveChanges();
}

public void Delete(int id=0){
  Contact contact = db.Contacts.Single(c=>c.ID == id);  
  db.Contacts.DeleteObject(contact);
}
~~~~

Thoạt nhìn thì các đoạn code như vậy không có vấn  đề gì cả. Tuy nhiên nếu các thao tác này lặp đi lặp lại sẽ gây ra issue sau:

1. Data access code bị lặp đi lặp lại khắp các nơi trong source code.

2. Source code trở nên khó thực hiện unit test. 

Những vấn đề trên có thể khắc phục bằng cách sử dụng Pattern Repository. Chúng ta sẽ tạo một Repository interface như sau:
~~~~
public interface IRepository<T> where T : class
  {
    IEnumerable<T> GetAll(Func<T, bool> predicate = null);
    T Get(Func<T, bool> predicate);
    void Add(T entity);
    void Attach(T entity);
    void Delete(T entity);
  }
~~~~
