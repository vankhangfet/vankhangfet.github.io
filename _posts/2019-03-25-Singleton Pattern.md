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

Cách này nhìn có vẻ đơn giản, tuy nhiên đây lại là badcode và không nên sử dụng vì nó không thread-safe. Chúng ta nên cải tiến lại một chút như sau:

~~~~
public sealed class Singleton
  {
    private static Singleton instance = null;
    private static readonly object padlock = new object();

    Singleton()
    {
    }

    public static Singleton Instance
    {
      get
      {
          lock (padlock)
         {
            if (instance == null)
             {
                 instance = new Singleton();
             }
          return instance;
         }
      }
    }
   }
~~~~

Cách này có vẻ hơi phức tạp một chút. Chúng ta hãy xem một cách thức khác triển khai đơn giản hơn. 

~~~~
public sealed class Singleton
  {
    private static readonly Singleton instance = new Singleton();

    // Explicit static constructor to tell C# compiler
    // not to mark type as beforefieldinit
    static Singleton()
    {
    }

    private Singleton()
    {
    }

    public static Singleton Instance
    {
       get
        {
        return instance;
         }
      }
  }
~~~~
