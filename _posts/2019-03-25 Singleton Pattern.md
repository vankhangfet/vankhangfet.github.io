---
layout: post
title: Singleton Pattern có đơn giản???
tags: [.Net]
---

Singleton Pattern là một design pattern rất hay được sử dụng. Tuy nhiên không phải lập trình viên nào cũng biết implement cho đúng. 
Với đa số lập trình viên, chúng ta sẽ implement như sau:

~~~~
public class Singleton
{
   private static Singleton instance ;
   
   private Singleton()
   {
   
   }
    
    public static Singleton SingletonInstance()
    {
      get{
           if(instance==null)
           {
              instance = new Singleton();
           } 
           return instance;
       }
    }
}
~~~~
