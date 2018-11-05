---
layout: post
title: C# - Extension Method
tags: [.Net]
---
C# - Extension Method là một additional method. Extension methods cho phép chúng ta inject thêm method vào trong class, mà không cần phải sửa class đó (Không cần phải modify trực tiếp, kết thừa, hoặc override). Extension method có thể cho custom class, framework class, hoặc 3rd class. 

Chúng ta hãy thực hành code một ví dụ dưới đây, để hiểu về Extension method. 

~~~~
int i = 10;

bool result = i.IsGreaterThan(100); //returns false
~~~~

Trong ví dụ này, ta sẽ thêm method IsGreaterThan() cho kiểu int. Các bước tạo ra extension method như sau:

~~~~
namespace ExtensionMethods
{
    public static class IntExtensions
    {

    }
}
~~~~

Ở đây chú ý là class IntExtension phải là static class và method cũng là static method. Ok, step1 chúng ta đã khai báo xong class, tiếp đến là khai báo method.

~~~~
namespace ExtensionMethods
{
    public static class IntExtensions
     {
        public static bool IsGreaterThan(this int i, int value)
        {
            return i > value;
        }
    }
}
~~~~
Với extension method thì parameter đầu tiên phải có tiền tố this. Ví dụ với extension cho kiểu float thì, parameter đầu tiên sẽ là this float i. Sau khi implement xong, chúng ta có thể dùng được extension method như ví dụ dưới đây

~~~~
using ExtensionMethods;

class Program
{
    static void Main(string[] args)
    {
        int i = 10;

        bool result = i.IsGreaterThan(100); 

        Console.WriteLine(result);
    }
}
~~~~

Có một điểm rất hay các bạn nên biết đó là "LINQ is built upon extension methods that operate on IEnumerable and IQeryable type."
Trong LINQ có rất nhiều extension method build trên kiểu dữ liệu là IEnumerable và IQueryable. Hy vọng qua bài viết này, các bạn đã biết cách sử dụng một extension method.



